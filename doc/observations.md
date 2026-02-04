Source: https://totalwarwarhammer.fandom.com/wiki/Combat?utm_source=chatgpt.com

The chance to hit is determined by the following calculation (attacker's attack skill vs. target's melee defense):

Chance to hit = ( 35 + (Icon stat attack Melee attack - Icon stat defence Melee defense) ) %

Each unit has a minimum 8% chance to hit after applying modifiers and a maximum of 90% (or 10% chance to miss). Stats are modified by fatigue levels before the calculation.



# Melee Combat Primer (and the Math Behind It) (source: https://www.reddit.com/r/totalwar/comments/dlmw4g/comment/f4s1b9l/?utm_source=share&utm_medium=web2x&context=3)

A small primer on melee combat and the math that governs it.

---

## Melee Attack and Melee Defense

**Melee Attack** measures how good your unit is at hitting an opposing unit.  
**Melee Defense** measures how good a unit is at avoiding getting hit.

Each melee swing uses a simple hit-chance formula:

- Base chance to hit: **35%**
- Add attacker’s **Melee Attack** (as a percentage increase)
- Subtract target’s **Melee Defense** (as a percentage decrease)

**Final hit chance is capped:**
- Maximum: **90%**
- Minimum: **8%**

**Flanking reduces defense:**
- Attacked from the **side**: target Melee Defense is reduced by **40%**
- Attacked from the **rear**: target Melee Defense is reduced by **75%**

These are still **percent chances**—there are no guaranteed hits or misses (as far as I’m aware).

---

## Weapon Damage and Armour

When an attack connects, it deals some combination of:

- **Armour-piercing damage (AP)**  
- **Non-armour-piercing damage (non-AP)**

You can see both by hovering over **Weapon Strength** on the unit card.

### Armour-piercing damage
- **Always applied**, regardless of armour.

### Non-armour-piercing damage and armour
- Armour reduces **some** non-AP damage.

The armour value shown on the unit card is the **maximum** percent reduction per hit.  
The **minimum** is **half** the displayed value.

A random value is rolled between min and max each time the unit is hit.

**Example:**
- Unit has **90 armour**
- Reduction roll range: **45% to 90%**
- If it rolls **75%**, then **75% of non-AP damage** is negated for that hit.

---

## Damage Resistances and Ward Save

After AP/non-AP + armour is resolved, **resistances** apply.

### Common resistances

- **Physical resistance:** reduces damage from non-magical attacks  
  - Example: Ethereal units (like **Syreens**) often have **no armour**, but may have **75% physical resistance**, making them extremely durable vs non-magical damage.

- **Fire resistance:** reduces damage from **flaming attacks**  
  - Example: **Irondrakes** and the **Flamespyre Phoenix** take **70% less damage** from fire attacks.

- **Magic resistance:** reduces damage from **magical attacks**  
  - Example: Many dwarf units have **25%** base magic resistance; some abilities add more.

- **Missile resistance:** reduces damage from **ranged attacks**  
  - Example: Many Lords/monsters have some missile resistance; various **Slann** (including **Mazdamundi** and **Kroak**) have **40% missile resistance**.

### Ward Save
- Reduces **all types of damage**.
- Usually granted by **skills, spells, or items**.

### How resistance totals work
- Applicable resistances are **added together** and reduce final damage by that total percent.
- Total reduction is capped at **90%**.
- Minimum damage dealt by an attack is **1**.

**Example:**
- Irondrakes have **35% magic resistance** and **70% fire resistance**
- If attacked by **Ikit Claw (on foot)** with **magical + flaming melee attacks**
- Total applicable resistance: **105%**
- Capped to **90%**
- Result: Irondrakes take **90% less damage** than normal from Ikit’s attacks

---

## Attack Types and Weaknesses

Attacks can include special modifiers:

- **Flaming**
- **Magical**
- **Poison**
- (No modifier = normal **physical** damage)

### Flaming attacks
- Deal increased damage vs units with **weakness to flaming attacks**
  - Examples: Tomb Kings Lords, regenerating units like trolls
- Some abilities can apply fire weakness (e.g., Huntsman General **Oil Flask**, Bright Wizard **Kindleflame**).
- Deal reduced damage vs units with **fire resistance**.

**Fire weakness** is a percentage and is applied in the same stage as resistances.  
It effectively **opposes** resistances; if weakness outweighs resistances, the unit takes **bonus damage**.

If a unit has **no fire weakness** and **no fire resistance**:
- The damage is treated as **physical**, and can be reduced by **physical resistance**.

### Magical attacks
- Do **not** increase damage by themselves.
- They **bypass physical resistance entirely**.
  - This is especially dangerous to Ethereal units that rely on physical resistance and typically have low/no armour.
- Magical attacks are reduced by **magic resistance**.

Some effects can lower magic resistance, but (as far as I can tell) this does **not** create a “weakness to magic” that causes bonus damage. Fire is the main weakness type.

If a unit has **no physical resistance** and **no magic resistance**, then magical damage isn’t reduced or amplified.

### Poison attacks
- Do not increase damage and have no special resistance interactions.
- Apply a debuff to the target:
  - Reduced **speed**
  - Reduced **damage**
  - Reduced **vigour**

---

## Bonus vs Infantry / Bonus vs Large

Some units have bonus values against either:

- **Infantry-sized** targets: infantry, most hounds, most foot Lords
- **Large** targets: cavalry and monsters (anything larger than the average person)

You can see whether a unit is “large” by the symbol on the unit card.

### What the bonus does

1. **Adds bonus damage**  
   The bonus is added to weapon strength while preserving the AP/non-AP ratio.

   **Example:**
   - Base damage: **20 AP** and **8 non-AP** (28 total)
   - Bonus vs Large: **+10**
   - New total: 38 damage  
     Ratio preserved → **26 AP** and **12 non-AP**

2. **Adds bonus Melee Attack**  
   The bonus value is also added to the unit’s **Melee Attack** when attacking that target type.

   In the example above, the unit gains **+10 Melee Attack** vs Large → effectively **~10% higher hit chance** vs large units.

**Summary:** Bonus vs Large/Infantry increases both **accuracy** and **damage** against that target type.  
This helps define battlefield roles (e.g., spearmen often have bonus vs large).

---

## Charge Bonus and Charge Defense

**Charge Bonus** works similarly to bonus-vs values:

- Increases **melee attack** and **weapon damage**
- Applies at full value during the **first second** of a charge
- Then reduces **linearly over the next 13 seconds**
- Charging units usually gain **increased speed** during the charge

### Charge defense traits
Polearm units often have:

- **Charge Defense vs Large:** negates the charge bonus of **large** charging units (usually cavalry)
- **Expert Charge Defense:** negates the charge bonus of **all** enemies  
  - Also believed to help prevent cavalry from penetrating through the unit

Charge defense only activates when:
- The unit is **not moving**
- It is charged **from the front**

---

## Splash Damage

Some units can hit multiple entities per melee swing: **splash damage**.

Units are limited by:
- **Max number of targets hit** per attack (e.g., Dread Saurian can hit **12**)
- **Target size restrictions**
  - Example: A **Banshee** can hit up to **3** targets, but only infantry-sized
  - A **Necrofex Colossus** can splash up to **10** targets of any size
- **Splash area** around the swing (larger units typically have larger splash areas)

### How damage is applied
- The unit’s weapon damage is **spread across all splash targets hit**
- Each splash hit is treated as a **separate attack**, applying all the same calculations (hit chance, armour, resistances, etc.)

**Practical example:**
If you want to take down **Wulfrik on a Mammoth** with a Lord/Hero:
- Wulfrik hits hard, but can splash up to **10** enemies
- Swarm him with infantry while your character fights him
- If splash is maximized, Wulfrik’s damage to your single character can be reduced by up to **10×** (since the damage is distributed)
- He’ll still mulch infantry, but your character gets to hit him for full damage

---

## Vigour and Fatigue

As units move and fight, they lose vigour and progress through fatigue levels.

As fatigue increases, units suffer reductions to several stats, including:
- Armour
- Speed
- Melee Attack
- Melee Defense
- Charge Bonus
- Reload Skill (for ranged units)

---
---

## Notes / Corrections (from discussion) 

### Charge Bonus duration
- **Correction:** Charge bonus *sticks around* after impact.
- It applies at **full value during the first second** of a charge, then **decays linearly over (by default) 15 seconds**.
- The decay duration can be **modded** to last a different amount of time.

> *“Good point about the charge bonus, it makes more sense that way. Especially for cavalry since they can penetrate and hit multiple units.”*

### Fatigue affects armour (important nuance)
- Fatigue **lowers armour**, so a unit with **100 armour** won’t always have the same reduction throughout a fight.
- When a unit is **Fresh**, the **displayed armour matches base armour**, so the armour-roll example works as expected at that state.

---

### Extra community note (unconfirmed / hard-to-source mechanics)
Some players mention potential quirks involving **Charge Distance / Adopt Charge Pose** in `battle_entities`, but confirmation is scarce. Information on related topics like **collision damage**, **impact damage**, and **charge bonus details** can be surprisingly hard to track down.

---
---

## Notes that make this document more complete (source): https://www.reddit.com/r/totalwar/comments/eddqsv/melee_combat_primer/

### Update history / context
- Includes a running **changelog** describing what was added or corrected over time:
  - Added **terrain types**
  - Corrected **splash damage** info
  - Removed **attack interval** section (attack interval alone is misleading without animation time)
  - Added **elevation**, plus **Strider** and **Woodsman**
  - Updated terrain interactions after CA simplifications
  - Updated for **The Twisted and the Twilight** DLC (Wood Elves now categorized as **Forest Stalkers** / **Large Forest Stalkers**)

### Terrain interactions (major completeness boost)
- Adds a full **terrain ruleset** focused on:
  - **Shallow water** and **forests**
  - Movement and melee penalties/bonuses by unit category
- Defines unit “terrain types” and their behavior:
  - small, small strider, small forest strider
  - large, large beast
  - aquatic small, aquatic large
  - ethereal
  - forest stalkers, large forest stalkers (Wood Elves)

### Elevation mechanics
- Adds uphill/downhill effects:
  - Speed changes when moving downhill/uphill
  - Up to **30%** damage swing in melee/ranged based on height differences (with different thresholds)
  - Fatigue gain increases uphill (up to **150%** more per tick)
- Notes that elevation is calculated per **entity/model**, not just the unit blob
- Calls out why this matters a lot for **cavalry** (charge impact relies on speed)

### Strider vs Woodsman
- Clearly distinguishes attributes:
  - **Strider:** ignores terrain penalties, ignores uphill penalties (speed/fatigue/combat), can move through trees, still benefits from downhill bonuses
  - **Woodsman:** can move through trees (only)

### Melee contact effects (on-hit debuffs)
- Adds mechanics for effects like:
  - poison, frostbite, armour sundering
- Clarifies these are not “bonus damage” and aren’t resisted like fire/magic—rather they apply **on hit**
- Provides a strong example: **Weeping Blades** (armour halved for **35 seconds**)

### Splash damage edge case: High Threat targeting
- Adds the “High Threat” exception to splash damage division:
  - Splash attacks can **focus full damage** on a high-threat entity instead of splitting it
- Summarizes the general rules:
  - Single-entity units (characters/monsters/war machines) are high threat
  - Chariots are high threat
  - Infantry/cavalry/artillery/monstrous infantry are not (with patch consistency notes)
- Corrects the common tactic assumption: swarming splash units with chaff doesn’t work the same if a high-threat entity is present

### Extra rule clarity and constraints
- Makes several boundaries explicit:
  - Melee attack/defense and armour **can’t go below 0**
  - Resistances are applied **additively**
  - “Only one weakness exists” claim: **fire weakness**
  - Minimum damage floor: **1**
  - Resistance cap: **90%**
  - Fire weakness can create bonus damage (capped at **+100%**)

---
# Comparison: Updated Notes vs CA Blog (Feature Focus #2: Damage, Part 1)

Source: CA blog — “Feature Focus #2: Damage (Part 1)”
https://community.creative-assembly.com/total-war/total-war-warhammer/blogs/6-feature-focus-2-damage-part-1

---

## ✅ Where your updated notes align with CA

- **Hit chance + caps**
  - Base **35%** to hit, modified by melee attack/defense
  - Final hit chance capped at **90% max / 8% min**

- **Flanking and rear attacks reduce defense**
  - Your “-40% side / -75% rear” matches CA’s framing:
    - Flank effectively multiplies melee defense by **0.6**
    - Rear effectively multiplies melee defense by **0.3**

- **Bonus vs Infantry/Large**
  - Adds to **melee attack** (hit chance) and **damage**
  - Bonus damage preserves the **AP vs base damage ratio**

- **Armour roll concept**
  - Armour reduction is rolled between **0.5× armour** and **1× armour**

- **Resistances stack additively + cap**
  - Applicable resistances are summed
  - Total reduction capped at **90%**

- **Magical attacks do not ignore armour**
  - Magical damage bypasses **physical resistance**
  - It **does not** bypass armour

---

## ⚠️ Where your updated notes conflict (or need a version caveat)

### 1) Charge bonus decay duration
- **Your note:** full value on first second, then decays over **15 seconds (default)**
- **CA blog:** decays linearly over **13 seconds** after the first second (with an example at 6.5s)

**Recommendation:** if your doc is WH2-specific, either:
- update to CA’s 13s model **or**
- label as “WH2 / patch / mod variance” if you have a reason for 15s.

### 2) “Minimum damage = 1” vs armour reducing base damage to 0
- Your earlier primer states a hit can’t deal less than **1** damage.
- CA explicitly says **base damage can be reduced to 0** by armour (no minimum on base damage).

**Recommendation:** clarify the distinction:
- *Base damage component* can hit **0**
- if you keep a “minimum 1” claim, specify whether it applies to **final total damage** (post-all steps) and verify by version.

---

## ➕ Completeness upgrades CA adds that your notes don’t include yet

### 1) Fire applies “On Fire” (healing reduction)
- Fire damage can apply **On Fire** for **10 seconds**
- On Fire **halves incoming healing**

### 2) CA separates *Magic* vs *Spell* damage and introduces Spell Resistance
CA uses three tags:
- **Fire**
- **Magic**
- **Spell**

Key distinctions:
- **Magic:** physical resistance does not apply
- **Spell:** physical resistance does not apply, and **Spell Resistance** *does* apply

Also important:
- Spell Resistance affects damage from spell sources (e.g., winds/vortexes/magic missiles),
  but not just “units having magical attacks” or “weapons granted magical attacks by a spell.”

### 3) Missile resistance applies to missiles *and explosions*
- Missile Resistance affects:
  - missile impacts (including magic missiles)
  - **explosions** (e.g., mortar shell explosions)

### 4) Excess damage does not spill over
- Damage beyond what’s required to kill the struck entity is **lost**
- It does not carry over to another entity

---

## Suggested quick edits to your doc (high value)
- Add a short **Fire = damage modifier + On Fire healing penalty** note
- Add **Spell damage** and **Spell Resistance** as separate from “Magic”
- Clarify missile resistance applies to **explosions**
- Add the **no spillover** rule near splash/high-threat discussion
- Resolve or caveat the **13s vs 15s** charge decay discrepancy

---
Community notes from discord pin

Stats that the game does not  really explain 101 (There are 4 messages of explanations):
Here is a list of different stats and traits that the game just throws at you, but doesn't really explain. Plan is to extend this list till all stats have been explained in some fashion. Some of these stats are not shown in game, but are present in the files and are shown on sites like TWWstats.

Units and Entities
Very short explanation since these words will be mentioned a lot. A unit is the entire regiment, while an entity is a single model in a unit. A unit of Empire Spearmen has 120 Entities etc.

Armour
Armour provides damage reduction to base weapon and base missile damage. The amount of reduction given to every instance of damage where armour applies, is a random percentage with a lower cap of half your armour and upper cap of all your armour. So if you have 100 armour, you reduce base damage with 50 to 100% 

Resistances
There are a plethora of different resistances to keep track of and they all cap at 90%! Resistances can in general not be negative either.
Here is a list and what they do:
Physical resistance reduces all non-magical damage. This means Magical Attacks (marked with a blue swirly) and Direct Spell damage bypasses this resistance
Missile resistance only works on missiles. It affects both regular and explosive missile damage.
Spellresistance works only towards spells. This has no effect on Magical Attacks in Total War: Warhammer 3!
Fire resistance works against any attack that has the Flaming attack marker. Fire resistance is the only exception where you can go into negative, with Weakness to Fire. They subtract directly from each other, so 50% Fire Resistance and 60% Weakness to Fire results in 10% Weakness to Fire. 
Ward save is also a resistance, sometimes just called Damage Reduction. This percentage cannot be bypassed (as of yet) and just flat out reduces all damage taken.

Missile Block
Gives the unit a chance to block certain missiles from the front. Any shots from the flank or the rear ignores this. The shield animation does not matter when it comes to whether it works or not (like with Quarrelers who has the shield on their back). The two different projectile types this does not work against is the Misc and Artillery type, unless the unit has Ballistic Plating, which specifically makes that unit able to block all types of missiles. Explosive missiles can only have it's regular missile damage blocked.
There is also 360 degree Missile block tags and Directional Missile Block, which makes you able to block from all sides (Directional Missile Block gets to block missiles from the flank at half chance and from the rear at 1/10th of the chance (70% missile block would be 35% and 7% respectively)

Speed and Acceleration/Deacceleration
Speed measures how fast a unit moves. Speed is seen in m/s at 1/10th of the speed value you have, so 32 speed means the unit runs at 3.2m/s. There are many units who can get a lot of speed, however speed is capped by the run animation of the unit. While we don't know any of those values, just be aware that stacking 300 speed on a lord may or may not have a lot of stats wasted as an example. 
Acceleration and Deacceleration is how fast a unit gets up to it's full speed and stops from full speed. Whenever a unit has to turn, it has to deaccelerate as well. While the exact effect of these two stats are not that easy to discern, Wayfarer is the most common trait which gives it, and has a very noticeable effect on how easy it is to manoeuvre the unit around. 

Melee Attack and Defence
Melee Attack (MA) and Melee Defence (MD) is used to calculate chance to hit for Melee attacks. The formula is:
35 + Attacker MA - Defender's MD
Hit chance is hard capped at 8% and 90%, which means you need 55 MA above your opponents MD to hit cap, and vice versa need 27 MD above your opponents MA to hit cap.