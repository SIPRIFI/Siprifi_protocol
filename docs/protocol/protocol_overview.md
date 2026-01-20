
<p align="center">
  <img src="../../assets/siprifi-logo.png" alt="Siprifi Logo" width="600
    ">
</p>

# Formal System Model and Binary Asset Solvency Buffer (BASB)

This section presents the formal mathematical specification of the Siprifi Finance protocol. Siprifi inherits the core collateralization, liquidation, and accounting mechanics of Aave V3, and introduces an additional solvency layer specifically designed for binary, highly correlatable assets such as prediction market outcome shares.

---

## 1. Collateral and Debt Definitions

Let $I$ be the set of collateral assets and $J$ the set of borrowed assets.

For each collateral asset $i \in I$:

- $C_i$: quantity of collateral  
- $P_i$: oracle price (USD)  
- $LTV_i \in (0,1)$: loan-to-value parameter  
- $LT_i \in (0,1]$: liquidation threshold  

Total collateral market value:

$$
V_C = \sum_{i \in I} C_i \cdot P_i
$$

Liquidation-adjusted collateral value:

$$
V_C^{liq} = \sum_{i \in I} C_i \cdot P_i \cdot LT_i
$$

For each borrowed asset $j \in J$:

- $D_j$: borrowed quantity  
- $P_j$: oracle price  

Total debt value:

$$
V_D = \sum_{j \in J} D_j \cdot P_j
$$

---

## 2. Health Factor and Liquidation Condition

The Health Factor (HF) is defined as:

$$
HF = \frac{V_C^{liq}}{V_D}
$$

A position is solvent if $HF \geq 1$ and liquidatable if $HF < 1$.

---

## 3. Base Borrowing Power

Base Borrowing Power (BBP) is computed as:

$$
BBP = \sum_{i \in I} C_i \cdot P_i \cdot LTV_i
$$

BBP represents the maximum debt allowed in the absence of Siprifi-specific risk constraints.

---

## 4. Collateral Grouping Structure

Collateral assets are partitioned into disjoint groups $g \subset I$ such that:

$$
\bigcup g = I \quad \text{and} \quad g_a \cap g_b = \varnothing \;\; \text{for} \;\; a \neq b
$$

Each group corresponds to:
- a single prediction market, or  
- a governance-defined correlated set of markets  

For each group $g$, its market value is:

$$
MV_g = \sum_{i \in g} C_i \cdot P_i
$$

Let $G_N$ denote the set of the $N$ largest groups ranked by $MV_g$.

---

## 5. Binary Asset Solvency Buffer (BASB)

The Binary Asset Solvency Buffer is defined as:

$$
BASB = \sum_{g \in G_N} MV_g
$$

The BASB represents capital explicitly reserved against the total failure of the largest collateral concentrations.

---

## 6. Effective Borrowing Power

Effective Borrowing Power (EBP) is defined as:

$$
EBP = \max \left( 0,\; BBP - BASB \right)
$$

Borrowing is constrained by:

$$
V_D \leq EBP
$$

This constraint is enforced ex ante and precedes liquidation logic.

---

## 7. Binary Long-Tail Risk Model (100% VaR)

Prediction market outcome shares are binary assets whose terminal value at resolution time $T$ satisfies:

$$
P_i(T) \in \{0, 1\}
$$

Siprifi explicitly models a conservative tail-risk event.

**Assumption A1 (Tail Event):**

$$
\forall g \in G_N : \quad MV_g(T) = 0
$$

This corresponds to a 100% Value-at-Risk (VaR) assumption on the $N$ largest collateral groups, assuming instantaneous loss, zero recovery, and no reliance on liquidation liquidity.

---

## 8. Solvency Under Tail Event

At any time $t < T$, the system enforces:

$$
V_D \leq BBP - \sum_{g \in G_N} MV_g
$$

Under Assumption A1, the remaining liquidation-adjusted collateral equals:

$$
V_C^{liq,rem}
= V_C^{liq} - \sum_{g \in G_N} (MV_g \cdot LT_g)
$$

Since $LT_i \leq 1$ for all assets:

$$
V_C^{liq,rem} \geq BBP - \sum_{g \in G_N} MV_g
$$

Combining the constraints:

$$
V_C^{liq,rem} \geq V_D
$$

Therefore:

$$
HF_{rem} = \frac{V_C^{liq,rem}}{V_D} \geq 1
$$

Thus, even if the $N$ largest collateral groups collapse to zero value, the protocol remains solvent and produces no bad debt.

---

## 9. Core System Invariant

For all users and all times:

$$
V_D \leq BBP - \sum_{g \in G_N} MV_g
$$

$$
HF \geq 1 \quad \text{under normal operation}
$$

$$
HF \geq 1 \quad \text{under Assumption A1}
$$

These conditions define the core solvency invariant of Siprifi Finance and enable prediction market shares to be safely integrated as collateral in a lending protocol.

