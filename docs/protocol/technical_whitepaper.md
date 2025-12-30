
**Whitepaper V2.0**
**Date: Dec 30, 2025**

**Abstract:**
Prediction markets represent a powerful mechanism for information aggregation and decentralized hedging. However, their growth and the participation of liquidity providers (often acting as "insurance sellers") are hampered by capital inefficiency. Under current models, capital used to underwrite one prediction market outcome is typically siloed and cannot be leveraged for other opportunities. Siprifi Finance introduces a novel lending protocol, built upon the robust foundations of Aave, designed to accept validated Yes/No shares from prediction markets as collateral. By introducing a unique risk-mitigation mechanism Siprifi Finance aims to significantly enhance capital efficiency of prediction markets and unlock new ways of hedging various risks for defi users as well as new place to allocate capital for competitive yield.

---

**1. Introduction: The Promise and Problem of Prediction Markets**

Decentralized prediction markets (e.g., Polymarket) have emerged as innovative platforms allowing users to speculate on or hedge against the outcomes of real-world events. They leverage the "wisdom of the crowd" to forecast future events, offering valuable insights and risk management tools. Participants can buy or sell "outcome shares" (e.g., "YES, Candidate A will win" or "NO, Smart Contract X will not be exploited").

Individuals or entities who provide liquidity to these markets, effectively underwriting the "insurance" against certain outcomes (by selling "YES" shares on an undesirable event, or buying "NO" shares), play a crucial role. However, their capacity is fundamentally limited by capital efficiency.

**The Core Problem: Siloed Capital and Inefficiency**
In the current paradigm, capital committed to backing shares in one specific prediction market is locked to that market. An "insurance seller" wishing to underwrite ten distinct, uncorrelated risks would need ten separate pools of capital. This is starkly different from traditional insurance, where diversified risk pooling allows for greater capital leverage. This inefficiency:
*   Limits the amount of liquidity available in prediction markets.
*   Reduces the potential returns for liquidity providers.
*   Increases cost of insurance for insurance buyers
*   Constrains the overall growth and utility of the prediction market ecosystem.

---

**2. Our Vision: Siprifi Finance protocol - A Liquidity Engine for Prediction Markets**

Siprifi Finance is a decentralized lending protocol designed to address the capital inefficiency inherent in current prediction market structures. By forking the battle-tested Aave V3 architecture, Siprifi Finance will allow users to:

*   **Deposit validated Yes/No outcome shares** from reputable prediction markets as collateral.
*   **Borrow assets (e.g., stablecoins)** against this collateral.
*   **Unlock liquidity**, enabling "insurance sellers" and traders to redeploy capital into new prediction market opportunities, other DeFi protocols, or for any other purpose.

Our vision is to create a synergistic relationship: Siprifi Finance will draw strength from the growing prediction market ecosystem, and in turn, fuel its expansion by providing much-needed capital efficiency.

### Market Operational Workflow
Below is the technical lifecycle of the risk markets that generate the collateral for the Siprifi protocol:
![Market Lifecycle and Use Cases](../../assets/workflow.drawio.svg)
---

**3. Core Mechanics: Adapting Aave for Prediction Market Shares**

Siprifi Finance will inherit many of Aave's core features, including its over-collateralized lending model, Loan-to-Value (LTV) ratios, liquidation thresholds, and Health Factor calculations. However, specific adaptations are necessary for prediction market shares:

*   **Collateral Eligibility:** Initially, Siprifi Finance will accept Yes/No shares from established prediction markets (e.g., Polymarket) for events with clear, objectively verifiable outcomes. Governance will play a key role in whitelisting eligible markets and share types.
*   **Price Oracles:** Robust and reliable price feeds are paramount. We will integrate with leading oracle providers capable of accurately pricing these often volatile and binary-outcome-approaching shares. The price of a share (e.g., a "YES" share trading at $0.30) will determine its collateral value.
*   **Standard Lending Operations:** Users will be able to deposit their eligible shares, see their collateral value, and borrow other assets based on the assigned LTV for that share type. Interest rates will be determined by supply and demand dynamics within Siprifi Finance's lending pools.

To visualize how the protocol "quarantines" dominant risks to maintain solvency:

![Figure 2: Siprifi Risk Engine & Concentration Offset Logic](../../assets/ConcentrationLogic.svg)

> **Note:** The subtraction of the N-largest groups ensures that even a 100% loss in a primary position does not trigger bad debt.
---

**4. The Siprifi Innovation: Diversification Requirement**

The unique nature of prediction market shares – their potential for binary outcomes (value going to $0 or $1 at resolution) and the temptation for users to make large, concentrated bets – necessitates an additional layer of risk management beyond standard LTVs.

Siprifi Finance introduces a novel rule for calculating a user's effective borrowing power:

**`EffectiveBorrowingPower = BaseBorrowingPower - Sum(MarketValueOf_N_LargestCollateralGroups)`**

Where:

*   **`BaseBorrowingPower`**: The borrowing power calculated using Aave's standard algorithm based on the total collateral value and LTV ratios.
*   **`Sum(MarketValueOf_N_LargestCollateralGroups)`**: This is a deduction representing the sum of the current market values of the user's "N" largest distinct collateral positions *or* "N" largest governance-defined correlated asset groups.
    *   **"N Largest Collaterals"**: "Biggest" is determined by the current market value of the collateralized shares for a specific event.
    *   **"Correlated Asset Groups"**: Crucially, Siprifi Finance governance will have the power to define groups of prediction market shares that are deemed highly correlated (e.g., shares on the outcomes of multiple, related sporting events; shares on different crypto assets highly exposed to the same systemic risk). Such a group will be treated as a *single collateral entity* for the purpose of identifying the "N Largest." The market value of the group will be the sum of the market values of its constituent shares.
    *   The value of **"N"** (e.g., 1, 2, or 3) will be a key risk parameter set by governance.

**Mechanics and Rationale:**

1.  **Protecting Protocol Solvency:** This rule directly mitigates the risk of bad debt arising from a user's largest, most concentrated positions resolving unfavorably and their collateral value plummeting to zero. By preemptively reducing borrowing power based on these concentrated risks, the protocol maintains a larger safety margin.
2.  **Incentivizing True Diversification:** Users are strongly incentivized to diversify their collateral across genuinely uncorrelated prediction market events. Concentrating collateral in a few large positions or in a set of correlated positions will directly and significantly reduce their borrowing capacity. To maximize borrowing power, users must spread their risk.
3.  **Adaptable Risk Management:** Governance can adjust "N" and the definitions of "Correlated Asset Groups" to respond to evolving market conditions and risk assessments.

**Example:**
A user deposits various prediction market shares. Aave's algorithm might calculate a total borrowing power of $10,000. If "N" is set to 1, and the user's largest single (or correlated group) collateral position has a market value of $3,000, their Effective Borrowing Power on Siprifi Finance becomes $10,000 - $3,000 = $7,000. If their two largest (N=2) positions/groups were valued at $3,000 and $2,000, their borrowing power would be $10,000 - ($3,000 + $2,000) = $5,000.

---

**5. Risk Management Framework**

Beyond the innovative borrowing power adjustment, Siprifi Finance will employ a multi-layered risk management strategy:

*   **Conservative LTV Ratios:** Prediction market shares will likely start with more conservative LTV ratios compared to more established crypto-assets, reflecting their unique volatility.
*   **Liquidation Mechanisms:** Standard Aave liquidation mechanisms will apply. If a user's Health Factor drops below the threshold, their collateral (Yes/No shares) will be made available for liquidators to purchase at a discount. Liquidators would then typically sell these shares on the native prediction markets. The protocol will explore partnerships or mechanisms to facilitate efficient liquidation of these specialized assets.
*   **Governance Oversight:** Key risk parameters, including LTVs, liquidation thresholds, the value of "N," oracle selection, and the crucial definitions of correlated asset groups, will be managed by Siprifi Finance governance.
*   **Safety Module/Treasury:** A portion of protocol fees may be allocated to a safety module or treasury to cover potential bad debt in extreme, unforeseen circumstances.

---

**6. Governance**

Siprifi Finance will be governed by its native token holders ([TokenSymbol], if applicable, or a DAO structure). Governance will be responsible for:

*   Whitelisting eligible prediction markets and share types for collateralization.
*   Setting and adjusting risk parameters (LTVs, liquidation thresholds, "N").
*   Defining and updating "Correlated Asset Groups."
*   Selecting and managing oracle providers.
*   Approving protocol upgrades.
*   Managing the protocol treasury and safety module.

A robust and active governance community will be crucial for the long-term security and adaptability of the protocol.

---

**7. Ecosystem Impact & Future Directions**

We believe Siprifi Finance will have a profound positive impact:

*   **For Prediction Market Liquidity Providers:** Unlocks significant capital, allowing for greater participation and higher potential returns.
*   **For Prediction Markets:** Fosters deeper liquidity, tighter spreads, and the creation of more diverse markets due to increased capital availability.
*   **For the Broader DeFi Ecosystem:** Introduces a new, valuable collateral type and a novel risk management paradigm.

Future directions may include:
*   Integration with a wider array of prediction platforms.
*   Developing more sophisticated tools for assessing correlation and risk.
*   Creating structured products based on prediction market share collateral.

---

**8. Conclusion**

Prediction markets hold immense potential, but their growth is tethered by capital inefficiency. Siprifi Finance offers a direct solution by enabling prediction market shares to be used as collateral within a modified Aave framework. Our innovative risk management approach, especially with governance-defined correlated asset grouping, provides a robust mechanism to manage the unique risks associated with this asset class while strongly incentivizing users towards genuine diversification.

Siprifi Finance aims to be more than just a lending protocol; it aspires to be a foundational liquidity layer that empowers the entire DeFi ecosystem, fostering greater participation, efficiency, and innovation.

---

**Disclaimer:**
This whitepaper is for informational purposes only and does not constitute an offer to sell, a solicitation of an offer to buy, or a recommendation of any security or any other product or service. The information contained herein has been obtained from sources believed to be reliable, but its accuracy and completeness are not guaranteed. Siprifi Finance is a work in progress and is subject to change. Participating in DeFi protocols involves significant risk, including the risk of loss of principal.

---
