
<p align="center">
  <img src="assets/siprifi-logo.png" alt="Siprifi Logo" width="600
    ">
</p>

# Protocol Overview: Siprifi Finance

## 1. Executive Summary
[cite_start]Siprifi Finance is a decentralized protocol designed to solve the structural liquidity failures of traditional protection markets, such as Credit Default Swaps (CDS) and insurance derivatives[cite: 5, 27]. [cite_start]While traditional OTC markets rely on static, bilateral contracts that lock capital for long durations, Siprifi re-architects risk into continuously tradable YES/NO primitives[cite: 29, 57, 67]. [cite_start]By integrating a lending layer with a proprietary risk engine, Siprifi enables protection issuers to collateralize their positions, unlocking capital efficiency that is impossible in legacy financial systems[cite: 18, 80].

---

## 2. From Static Contracts to Marketized Risk
[cite_start]Siprifi moves away from "one-sided" insurance models where liquidity disappears during periods of stress[cite: 34, 55].

* **Tradable Primitives**: Protection is represented by binary outcome shares. [cite_start]A "NO" share represents the non-occurrence of an adverse event and serves as the primary instrument for protection issuers[cite: 68, 71].
* [cite_start]**Continuous Price Discovery**: Unlike OTC derivatives that lack transparency, Siprifi shares are marked-to-market and freely transferable, attracting speculators who provide liquidity when hedgers retreat[cite: 48, 63, 75].
* [cite_start]**Two-Sided Markets**: By embracing speculation as a stabilizing force, the protocol ensures markets remain functional even during volatile "death spiral" conditions that typically freeze traditional markets[cite: 41, 62, 86].



---

## 3. The Siprifi Risk Engine: Effective Borrowing Power (EBP)
[cite_start]The protocol’s core innovation is its ability to treat "illiquid" risk as productive collateral without risking protocol solvency[cite: 9, 81].

### The Concentration Offset Logic
Because binary outcomes (YES/NO) can drop to zero, Siprifi employs a conservative borrowing power adjustment.

**The Formula:**
`EffectiveBorrowingPower = BaseBorrowingPower - Sum(MarketValueOf_N_LargestCollateralGroups)`

* **Solvency Buffer**: The protocol subtracts the value of the $N$ largest risk exposures from a user's total borrowing capacity.
* **Diversification Incentive**: This formula mathematically forces protection issuers to diversify their underwriting across uncorrelated risks to maximize their liquidity.
* **Correlated Risk Groups**: Governance defines "Risk Groups" (e.g., systemic financial failures or related credit events) to ensure that highly correlated assets are treated as a single concentrated exposure.

---

## 4. Capital Efficiency Workflow

### 1. Risk Underwriting (Issuance)
[cite_start]An issuer provides protection by acquiring **NO shares** for a specific credit or adverse event[cite: 71]. [cite_start]Instead of capital sitting idle in escrow, the issuer holds a mark-to-market position[cite: 31, 72].

### 2. Collateralization
[cite_start]The issuer deposits these NO shares into the Siprifi lending pool[cite: 80]. The protocol calculates the EBP based on the current market price of the risk.

### 3. Liquidity Redeployment
[cite_start]The issuer borrows stablecoins against their underwriting positions to issue *new* protection contracts or participate in other DeFi markets, significantly increasing capital velocity[cite: 81, 82].

---

## 5. Crisis Resilience & Settlement
[cite_start]Siprifi is designed to remain active when traditional protection sellers disappear[cite: 85, 92].

* **Liquidity Persistence**: Fear becomes a source of liquidity. [cite_start]As risk rises, the widening spreads and volatility attract arbitrageurs and traders[cite: 86, 87].
* **Automated Liquidation**: Oracles track the real-time probability of the adverse event. If the probability of a "YES" outcome rises sharply, under-collateralized "NO" positions are liquidated to protect lenders.
* **Settlement**: Upon event resolution, winning shares are redeemed for the underlying assets, and debt is settled programmatically, removing the need for manual claims processing or bilateral trust.

---

## 6. Governance & Risk Controls
The DAO manages the "Risk Parameters" that safeguard the protocol:
* **Asset Whitelisting**: Onboarding new risk primitives and credit events.
* [cite_start]**Correlation Mapping**: Identifying systemic links between different protection markets[cite: 89].
* **LTV & N-Value**: Adjusting the number of subtracted groups ($N$) based on global market volatility.

---
*Copyright © 2025 Siprifi. All rights reserved. Logic protected under Siprifi Risk Engine Intellectual Property.*