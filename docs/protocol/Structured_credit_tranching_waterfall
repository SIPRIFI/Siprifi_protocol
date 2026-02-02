# Siprifi Technical Paper: The Risk Waterfall & Credit Tranching

## 1. Executive Summary: The Credit Transformation
Siprifi transforms binary **Outcome Shares** (prediction market tokens) into **Structured Credit Primitives**. This is achieved by segmenting the liquidity pool into layers with different risk-absorption priorities, known as **Tranches**. 

Unlike traditional prediction markets where capital is "locked," Siprifi’s architecture creates a dynamic environment where liquidity providers (LPs) earn yield based on the "Insurance" (CDS) they provide to the market.

---

## 2. The Capital Stack: Senior vs. Junior

The protocol organizes all deposited assets into a vertical hierarchy. This determines the priority of payments and the order of loss absorption.

### 2.1 Junior Tranche (The Risk Anchor)
* **Collateral:** Primarily **NO-tokens** (Outcome Shares) and a minority of stables.
* **Role:** The **First-Loss Capital**. It acts as the "equity" layer of the pool.
* **Incentive:** Residual Yield Capture. It receives the majority of premiums after Senior obligations are met.
* **Function:** It is the core engine of the CDS market. Without the Junior Tranche, the protocol cannot issue "YES" protection.

### 2.2 Senior Tranche (The Liquidity Backstop)
* **Collateral:** Stablecoins (USDC/USDT) or Blue-chip assets (ETH).
* **Role:** **Protected Liquidity**. It ensures immediate, fungible cash flow for claim settlements.
* **Incentive:** Prioritized, low-volatility APR.
* **Function:** Provides market depth, allowing institutional protection buyers to enter the system with confidence.



---

## 3. The Yield Waterfall (Cash Flow Logic)

The "Waterfall" defines the path of premiums paid by protection buyers. It ensures that the Senior layer is satisfied before the Junior layer captures its leveraged upside.

### 3.1 Flow of Premiums (Yield Distribution)

1.  **Protocol Fee:** A flat fee is deducted for the Siprifi DAO treasury.
2.  **Senior Priority Return:** A pre-defined APR (e.g., 5%) is distributed to the Senior Tranche.
3.  **Junior Residual Capture:** 100% of the remaining premiums flow to the Junior Tranche. Because the Junior Tranche is typically smaller than the Senior, the yield is **mathematically leveraged**.

### 3.2 Loss Absorption (Settlement Priority)

When an event is triggered (e.g., a "YES" outcome occurs), the protocol settles the claim:

1.  **Liquidity Drawdown:** The payout is executed using the liquid reserves (Senior Tranche cash).
2.  **NAV Devaluation:** To "repay" the pool, the **Net Asset Value (NAV)** of the Junior Tranche is reduced. The Junior layer acts as a shield, preventing the Senior's principal from being affected.



---

## 4. Mathematical Solvency: The SCE Guardrail

To ensure the Senior Tranche is never at risk, the **Structured Credit Engine (SCE)** enforces a strict limit:

$$Total\,YES\,Exposure \le Junior\,Tranche\,Value \times EBP$$

The **EBP (Effective Borrowing Power)** adjusts based on the **Maturity Gap** ($T_{exp} < T_{liq}$). This ensures that the Junior Tranche always has sufficient value to cover 100% of the issued protection before the event resolution.

---

## 5. Numerical Execution Example

### Scenario: The Macro-Volatility Pool
* **Total Pool Size:** $1,000,000
* **Senior Tranche (USDC):** $900,000 (90%)
* **Junior Tranche (NO-tokens):** $100,000 (10%)
* **Annual Premiums (from YES buyers):** $150,000

#### Case A: No Event Occurs (Yield Focus)
* **Senior Payout (5% fixed):** $45,000
* **Junior Payout (Residual):** $150,000 - $45,000 = **$105,000**
* **Result:** The Junior Tranche earns **105% APR** on its $100k capital, while the Senior earns its stable 5%.

#### Case B: Event Occurs (Loss Focus)
* **Claim Payout:** $80,000 must be paid to protection buyers.
* **Senior Impact:** $0 (Principal remains at $900,000).
* **Junior Impact:** NAV drops from $100,000 to **$20,000**.
* **Result:** The Junior Tranche absorbed 100% of the shock, protecting the institutional capital.



---

## 6. Strategic Conclusion: Why Tranching?

1.  **For NO-Holders:** They transform "static" tokens into professional insurance underwriting assets with leveraged yield.
2.  **For Institutional LPs:** They access "Real Yield" uncorrelated with crypto prices, protected by a massive capital buffer (The Junior Tranche).
3.  **For the Ecosystem:** Siprifi creates **Secondary Liquidity** (via sipUSD), allowing users to exit their "tranche positions" at any time without waiting for event resolution.
