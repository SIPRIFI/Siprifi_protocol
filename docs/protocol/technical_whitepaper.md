<p align="center">
  <img src="../../assets/siprifi-logo.png" alt="Siprifi Logo" width="600">
</p>

# Siprifi Finance: Whitepaper V3
**Version:** 3.1.0 (Technical Deep-Dive)  
**Date:** January 24, 2026  
**Status:** Confidential / Technical Specification

---

## 1. Abstract: The Evolution of Risk Primitives

Decentralized prediction markets have demonstrated their ability to encode collective beliefs and price binary outcomes on-chain. 

However, despite their informational value, current prediction market designs remain structurally inefficient as mechanisms for risk transfer. Capital is locked until resolution, exposures are siloed, maturities are flat, and correlated risks are treated independently, leading to poor capital efficiency and fragile liquidity under stress.

Siprifi introduces a decentralized structured credit protocol that repurposes prediction market outcome shares into reusable, risk-aware credit instruments. By combining binary YES/NO exposures with principles derived from credit default swaps (CDS), maturity segmentation and tranches form (CDO’s), and strict decorrelation constraints, Siprifi enables capital-efficient protection markets without relying on traditional leverage, margin trading, or reactive liquidations.

The protocol treats outcome shares not as speculative positions, but as time-bound credit exposures with deterministic settlement paths. Long-duration, strongly collateralized positions form the senior risk layer, while short-duration, NO-backed exposures operate as junior tranches constrained by correlation, maturity, and system-wide credit capacity.

 Losses are absorbed locally, preventing cascading insolvency across unrelated risks.

Siprifi is not a prediction market, nor a leverage platform.
It is a credit structuring engine for decentralized risk, designed to make on-chain protection markets composable, solvent, and economically intelligible under worst-case assumptions


---

## 2. The Structured Credit Engine (SCE)

The core of Siprifi is the **Structured Credit Engine (SCE)**, which manages the lifecycle of protection-selling positions.


![Liquidation Mechanism](../assets/No-as-collateral.svg)

### 2.1 The Credit Capacity Framework
Siprifi moves away from simple LTV (Loan-to-Value) ratios, which fail to account for event-based volatility. Instead, it utilizes **Effective Base Power (EBP)**.

$$
V_C = \sum_{i \in I} C_i \cdot P_i
$$

$$
EBP = \max \left( 0,\; BBP - BASB \right)
$$

**Where:**

- $V_C$: Total market value of the collateral.
- $C_i$: Quantity of collateral asset $i$.
- $P_i$: Oracle price of asset $i$.
- $EBP$: Effective Borrowing Power.
- $BBP$: Base Borrowing Power.
- $BASB$: Binary Asset Solvency Buffer.
- $B_k$: A *risk bucket* representing a group of correlated events or assets.
- $\max(B_k)$: Maximum potential loss within a given correlation cluster.


### 2.2 Risk Bucket Aggregation
Assets are not treated individually. They are assigned to **Correlation Groups ($G$)**. 
If $Asset_A$ and $Asset_B$ have a historical or logical correlation $> 0.7$, they occupy the same bucket.
$$Loss_{Bucket} = \sum (Exposure_i \cdot \text{Correlation Factor}_{ij})$$

---

## 3. Maturity and Duration Matching (The "Safety Valve")

To prevent systemic insolvency, Siprifi enforces a **Maturity Gap Constraint**. 

> **Protocol Rule:** The weighted average maturity of the protection sold (Junior Tranche) must always be shorter than the liquidation profile of the collateral (Senior Tranche).

$$T_{exp}(Protection) + \Delta t < T_{liq}(Collateral)$$

This ensures that the protocol has a "time buffer" to resolve short-term event outcomes before the underlying long-term collateral can be significantly impaired by market volatility.

---

## 4. Economic Unit: sipUSD & NAV Accounting

Siprifi operates as a **Non-Redeemable Closed-Loop System**. Value is tracked via **Net Asset Value (NAV)**.

### 4.1 System NAV Formula
The protocol's real value is calculated at every oracle heartbeat:

$$NAV_{sys} = \frac{(A_{res} + \sum V_{shares} + P_{accrued}) - L_{total}}{S_{sipUSD}}$$

Where:
* $A_{res}$: Reserve Assets (ETH/USDC).
* $V_{shares}$: Fair market value of active NO/YES shares held by the protocol.
* $P_{accrued}$: Accumulated premiums from protection buyers.
* $L_{total}$: Outstanding system liabilities.
* $S_{sipUSD}$: Total supply of sipUSD.

### 4.2 sipUSD as an Equity Proxy
sipUSD is a **Residual Claim Token**. 
* When a protection event **does not occur**, the "NO" shares expire worthless for the buyer, and the collateral is retained by the protocol.
* This results in **NAV Accretion**, making each sipUSD represent a larger share of the protocol's ETH reserves.

---

## 5. The Risk Waterfall (Loss Absorption)

Siprifi utilizes a three-tier waterfall to protect senior participants:

1. **First Loss Piece (Junior Tranche):** * Composed of users locking "NO" shares (Protection Sellers).
   * Losses result in immediate **sipUSD dilution**.
2. **Mezzanine (Protocol Reserve):** * A buffer funded by a percentage of all premiums ($P_{accrued}$).
3. **Senior Tranche (ETH Backstop):** * The core ETH collateral. This layer is only touched if the Junior and Mezzanine layers are fully exhausted ($NAV_{sys} \to 0$).

---

## 6. Mathematical Liquidation Logic

Liquidations are triggered when a Risk Bucket's potential loss exceeds the allocated Junior Tranche buffer.

**Trigger Condition:**
$$\frac{ECC}{V_{base}} < \text{Liquidation Threshold} (\gamma)$$

When triggered, the SCE executes a **Targeted De-risking**:
1. It identifies the Risk Bucket with the highest $B_k$.
2. It auctions the shares of that specific bucket in the underlying prediction market (e.g., Polymarket/Augur).
3. The proceeds are used to restore the $ECC$.

---

## 7. Strategic Advantages

* **Capital Efficiency:** Enables users to "stack" uncorrelated risks on a single capital base.
* **Risk Transformation:** Converts binary "bets" into institutional-grade credit instruments.
* **Stability:** By eliminating the external peg of sipUSD, the protocol is immune to the "death spirals" seen in algorithmic stablecoins.

---

## 8. Conclusion

Siprifi Finance represents the transition of DeFi from speculative gambling to **structured financial engineering**. By applying credit market principles—tranching, duration matching, and correlation analysis—to prediction markets, we unlock the most capital-efficient protection market in the ecosystem.

---

### Disclaimer
Siprifi is a structured credit protocol involving high risk. Technical specifications are subject to governance updates.

> **Proprietary Document — Copyright © 2026 Siprifi** > All intellectual property rights, including SCE formulas and sipUSD NAV logic, are exclusively owned by Siprifi.
