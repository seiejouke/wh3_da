# Unit-to-Unit Combat Simulation Equation (Readable Version)

You *can* deduce a workable combat equation from the mechanics you gathered. Below is a clean “expected damage per second” model you can use for unit-vs-unit simulation (and you can optionally swap parts for Monte Carlo rolls).

---

## 1) Hit chance per swing

**HitChance = clamp(35% + MeleeAttackEff − MeleeDefenseEff, 8%, 90%)**

Where:

- **MeleeAttackEff** = MA + BonusVs + ChargeBonus(t) + (buffs/terrain/fatigue MA changes)
- **MeleeDefenseEff** = MD * FlankMultiplier + (buffs/terrain/fatigue MD changes)

Flank multipliers:
- Front: **1.0**
- Side: **0.6**
- Rear: **0.3**

So in one line:

HitChance = clamp((35 + MA_eff − MD_eff) / 100, 0.08, 0.90)

---

## 2) Charge bonus over time

ChargeBonus contributes to BOTH:
- hit chance (as added MA)
- weapon damage (as added damage)

Simple model:

- Full bonus for the first **1 second**
- Then it decays linearly for **T seconds** (CA uses 13; you can parameterize it)

ChargeBonus(t):
- if t ≤ 1: CB0
- if 1 < t < 1 + T: CB0 * (1 − (t − 1)/T)
- if t ≥ 1 + T: 0

---

## 3) Weapon damage (Base + AP), preserving AP ratio

Split weapon strength into:
- **BaseDamage** (non-AP): DB
- **ArmorPiercingDamage**: DAP

TotalDamage = DB + DAP  
APRatio = DAP / (DB + DAP)

Let **X = BonusVs + ChargeBonus(t)** be the additive bonus damage.

To preserve the AP/Base ratio:

- BaseDamage' = DB + (1 − APRatio) * X
- APDamage'   = DAP + APRatio * X

This matches the “ratio preserved” behavior described in your notes/CA.

---

## 4) Armor reduces Base damage only (random roll)

Armor does NOT touch AP damage.

Armor roll:
- pick a random percent reduction between **0.5 * Armor** and **1.0 * Armor**
- cap reduction at **100%**

Then:

- BaseAfterArmor = BaseDamage' * (1 − ArmorRoll)
- APAfterArmor   = APDamage' (unchanged)

### Fast expected-value shortcut
If you want deterministic simulation:

ExpectedArmorRoll ≈ min(0.75 * Armor, 1.0)

So:

BaseAfterArmor ≈ BaseDamage' * (1 − ExpectedArmorRoll)

---

## 5) Apply resistances (additive, capped)

Let ResistSum be the sum of all resistances that apply:

Always:
- WardSave

If attack is Fire:
- add FireResistance (or negative value for FireWeakness)

If attack is NOT magical/spell:
- add PhysicalResistance

If attack is Magical:
- PhysicalResistance does NOT apply (it’s bypassed)
- MagicResistance may apply (depending on the game’s resistance definitions)

If attack is Spell-type:
- SpellResistance applies (separate axis in CA’s blog)

If attack is Missile/Explosion:
- MissileResistance applies

Then:

ResistSum is capped at **0.90** (90% reduction)

FinalDamagePerHit = (BaseAfterArmor + APAfterArmor) * (1 − clamp(ResistSum, MinResist, 0.90))

Where:
- MinResist can be negative if you allow weakness to increase damage
- If you want a simple cap like “max +100% damage”, set MinResist = −1.0

---

## 6) Expected damage per swing

ExpectedDamagePerSwing = HitChance * FinalDamagePerHit

This is the core “per swing” equation.

---

## 7) Unit-to-unit DPS (aggregate model)

Now scale by how many entities are actually swinging.

Let:
- nA(t) = number of attacker entities currently able to attack
- swingsPerSecond = attack frequency per entity (empirical constant)
- splashDivisor k(t) = how many targets the attacker’s damage is divided across (≈1 for single-target; >1 for splash splitting)

Then:

DPS_A_to_B(t) = nA(t) * swingsPerSecond * (ExpectedDamagePerSwing / k(t))

---

## 8) Time stepping (simulation loop)

For timestep Δt:

HP_B(t + Δt) = HP_B(t) − DPS_A_to_B(t) * Δt  
HP_A(t + Δt) = HP_A(t) − DPS_B_to_A(t) * Δt

To make it behave like the game:
- convert HP loss into entity deaths → reduces nA(t), nB(t)
- update flank state, charge state, fatigue state, terrain state over time
- update splash divisor based on contact + “high threat” rules (if modeled)

---

## Minimal “single equation” view

If you want the whole thing collapsed:

ExpectedDPS_A_to_B
= nA * freqA
  * HitChance(MA,MD,flank,BV,CB,mods)
  * Damage(DB,DAP,BV,CB,Armor,Resists)
  / splashDivisor

---

If you tell me whether you want **expected-value** (fast) or **Monte Carlo** (roll hit + armor per swing), I can express the exact same model as pseudocode in a repo-friendly block.
