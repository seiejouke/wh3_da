# Deducing a Unit-to-Unit Combat Equation (from the gathered rules)

Yes — you can build a practical unit-to-unit simulator from these mechanics. Below is a clean formulation that works either as a **stochastic (Monte Carlo)** model or an **expected-value** approximation.

---

## 1) Per-swing hit probability

For one attacker entity swinging at one target entity:

\[
p_{\text{hit}}=\text{clamp}\Big(\frac{35 + MA_{\text{eff}} - MD_{\text{eff}}}{100},\ 0.08,\ 0.90\Big)
\]

Where:

\[
MA_{\text{eff}} = MA + BV + CB(t) + \Delta MA
\]
\[
MD_{\text{eff}} = MD \cdot m_{\text{flank}} + \Delta MD
\]

- \(MA\): melee attack  
- \(MD\): melee defense  
- \(BV\): bonus vs (infantry/large) when applicable  
- \(CB(t)\): charge bonus contribution at time \(t\)  
- \(\Delta MA, \Delta MD\): fatigue / terrain / buffs / debuffs  
- \(m_{\text{flank}}\in\{1,\ 0.6,\ 0.3\}\) for front / side / rear (CA framing). 

---

## 2) Charge bonus decay model

CA’s description: full value immediately, then decays linearly after a successful charge. 

A simple piecewise model (parameterize the decay length \(T\)):

\[
CB(t)=
\begin{cases}
CB_0 & t\le 1 \\
CB_0\cdot\Big(1-\frac{t-1}{T}\Big) & 1<t<1+T \\
0 & t\ge 1+T
\end{cases}
\]

- If you follow CA’s stated default, set \(T=13\).   
- If you want to support mod variance, keep \(T\) as a tunable parameter.

---

## 3) Per-swing raw damage (Base + AP), preserving AP ratio

Let:
- Base (non-AP): \(D_B\)
- Armour-piercing: \(D_{AP}\)
- Total: \(D_T = D_B + D_{AP}\)
- AP ratio: \(r = \frac{D_{AP}}{D_T}\)

If an additive damage bonus \(X\) applies (from **Bonus vs** and/or **Charge Bonus**), CA adds it while preserving the AP/Base ratio. 

\[
D_B' = D_B + (1-r)\,X
\]
\[
D_{AP}' = D_{AP} + r\,X
\]

Commonly:
\[
X = BV + CB(t)
\]
(+ any similar additive damage sources you include)

---

## 4) Armour reduces Base damage only (random roll)

CA: armour rolls between **0.5×Armour** and **1×Armour**, and Base damage can be reduced to **0** (no minimum for Base). 

### Stochastic per-hit armour roll
\[
R \sim \text{Uniform}(0.5A,\ A)
\]
\[
R \leftarrow \min(R, 100)
\]
\[
D_B'' = D_B' \cdot (1 - R/100)
\]
\[
D_{AP}'' = D_{AP}'
\]

### Expected-value shortcut (fast sim)
\[
\mathbb{E}[R] \approx \min(0.75A, 100)
\]
\[
\mathbb{E}[D_B''] = D_B' \cdot (1 - \mathbb{E}[R]/100)
\]

---

## 5) Tags + resistances (additive, capped)

CA: resistances add together and cap at **90%** reduction; Magic/Spell have specific interactions with physical resistance; missile resistance applies to missiles and explosions. 

Define an effective reduction \(S\) (as a fraction), built from the resistances that apply:

- **Ward save** always applies
- **Physical resistance** applies only if the attack is *not* Magic or Spell
- **Fire resistance/weakness** applies only if attack has Fire tag
- **Spell resistance** applies only to Spell-tag damage sources
- **Missile resistance** applies only to missiles/explosions

\[
S = \text{clamp}\Big(\sum R_i,\ S_{\min},\ 0.90\Big)
\]

Then:
\[
D_{\text{after res}} = (D_B'' + D_{AP}'')\cdot(1 - S)
\]

Notes:
- Fire weakness can make \(S\) negative (bonus damage). CA discusses fire weakness as a negative resist.   
- If you want a hard cap on bonus damage (e.g., +100%), set \(S_{\min}=-1.0\) as a simulation parameter.

Fire’s extra “On Fire” effect (healing halved for 10s) is better modeled as a status effect separate from damage. 

---

## 6) Expected damage per swing

\[
\mathbb{E}[d_{\text{swing}}] = p_{\text{hit}}\cdot \mathbb{E}[D_{\text{after res}}]
\]

- Deterministic sim: use expected armour roll \(\mathbb{E}[R]\)
- Monte Carlo sim: sample hit/miss and armour roll each swing

---

## 7) From entity-vs-entity to unit-vs-unit DPS

Let:
- \(n_A(t)\): number of attacker entities able to attack at time \(t\)
- \(f_A\): swings per second per entity (empirical; roughly inverse of attack cycle)
- \(k(t)\): effective number of targets hit by splash division (≈ 1 if no splash or high-threat focus)

Then expected DPS from unit A to unit B:

\[
DPS_{A\to B}(t)= n_A(t)\cdot f_A \cdot \frac{\mathbb{E}[d_{\text{swing}}(t)]}{k(t)}
\]

---

## 8) Unit HP update (discrete timestep)

For timestep \(\Delta t\):

\[
HP_B(t+\Delta t) = HP_B(t) - DPS_{A\to B}(t)\,\Delta t
\]
\[
HP_A(t+\Delta t) = HP_A(t) - DPS_{B\to A}(t)\,\Delta t
\]

To make this behave like the game, you typically also:
- convert HP loss into **entity deaths**, reducing \(n_A(t)\) and \(n_B(t)\)
- update engagement/contact conditions affecting how many entities can swing

---

## What this gives you

- A clean **expected-value simulator** (fast, deterministic) using \(\mathbb{E}[R]\) and averaged splash behavior.
- A higher-fidelity **Monte Carlo simulator** sampling hit + armour + splash targeting each swing tick.

---
