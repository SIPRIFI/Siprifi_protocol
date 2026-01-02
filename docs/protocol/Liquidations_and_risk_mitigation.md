# Liquidation and Risk Mitigation

## 1. Overview
The Siprifi protocol operates on a principle of marketized risk rather than static insurance. Because prediction market outcome shares can experience rapid price movements and binary terminal outcomes (value going to $0 or $1), the protocol employs aggressive liquidation and mitigation strategies to ensure permanent solvency and liquidity.

---

## 2. Liquidation Mechanics
Liquidation is the automated process of seizing and selling a borrower's collateral when their position's risk profile becomes unsustainable.

### The Trigger: Health Factor ($H_f$)
Liquidation is triggered when a user's **Health Factor** drops below 1.0. Unlike standard lending protocols, Siprifi's $H_f$ is "concentration-aware".

$$H_f = \frac{\sum (Collateral_i \times LTV_i \times LiquidaitonThreshold_i) - ConcentrationOffset}{Total Borrowed}$$

* **Concentration Offset**: This is the market value of the user's $N$ largest correlated risk groups. By subtracting this value from the numerator, the protocol ensures that even if the user's largest bet fails completely, the remaining diversified collateral is sufficient to cover the debt.

### Liquidation Incentives
To guarantee that liquidations occur even during extreme volatility:
* **Liquidation Bonus**: Liquidators purchase seized shares at a governance-defined discount (e.g., 5-10%), incentivizing immediate arbitrage.
* **Flash Loan Support**: Siprifi is designed to support atomic, zero-capital liquidations via flash loans, allowing bots to clear bad debt without holding the underlying assets.

![Liquidation Mechanism](../../assets/liquidation.svg)
---

## 3. Risk Mitigation Strategies
Siprifi's resilience where traditional markets (like CDS) fail is due to several integrated layers of mitigation.

### 3.1 Marketized Liquidity
In traditional systems, crises cause issuers to vanish and markets to freeze. In Siprifi, **fear becomes a source of liquidity**.
* **Two-Sided Participation**: The protocol allows speculators and arbitrageurs to enter when hedgers retreat, ensuring continuous price discovery.
* **Tradability**: Because NO shares are mark-to-market and tradable, liquidity is sustained by market dynamics rather than the "goodwill" of protection sellers.

### 3.2 Protocol-Level Safeguards
* **Conservative LTV Ratios**: Baseline borrowing power is restricted to provide a significant safety buffer against price swings.
* **Correlated Risk Groups**: Governance defines groups of assets that share systemic risk (e.g., related credit events). These are treated as a single concentrated exposure to prevent a user from bypassing the diversification requirement.
* **Safety Modules**: A specialized module is designed to absorb extreme "tail events" where standard liquidations may be insufficient.

### 3.3 terminal Event Handling
As a prediction market approaches its "expiry" (resolution), the protocol mitigates the risk of binary collapse:
* **LTV Decay**: As the resolution date nears, the protocol may reduce the LTV for those shares to prevent new high-leverage positions from being opened on a "cliff" event.
* **Automated Settlement**: Winning shares are automatically redeemable for the underlying assets, ensuring that liquidators and lenders are made whole immediately upon event resolution.

![Risk farming loop](../../assets/Risk-Farmingloop.svg)

---

## 4. Governance Role in Mitigation
The Siprifi DAO is responsible for the active management of risk parameters:
1. **Setting $N$**: Adjusting the number of "Largest Positions" subtracted from borrowing power.
2. **Whitelisting**: Ensuring only validated, objectively verifiable prediction markets are accepted as collateral.
3. **Updating Correlation Maps**: Identifying new systemic links between different risk instruments.

---
*Proprietary Risk Management Framework - Copyright © 2026 Siprifi*
