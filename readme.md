<p align="center">
  <img src="assets/siprifi-logo.png" alt="Siprifi Logo" width="600">
</p>
## License

Copyright (c) 2026 Siprifi. All rights reserved.

This software and its associated documentation (the "Work") are the exclusive intellectual property of Siprifi. 

Access to this repository is granted for viewing and informational purposes only. No license is granted for:
1. Modification, reproduction, or redistribution of the Work.
2. Commercial use or use in secondary projects.
3. Creation of derivative works based on the unique formulas, diagrams, or logic contained herein.

Any unauthorized use, including but not limited to the use of the "Siprifi Risk Engine" or "Effective Borrowing Power" logic in other protocols, may result in legal action. 

For inquiries regarding commercial licensing or permissions, please contact: siprifinance@gmail.com 


# Siprifi Finance

**Siprifi Finance is a decentralized structured credit and clearing protocol for binary risk markets.**

Siprifi enables prediction market exposures to be issued, structured, and settled using pre-funded capital, hierarchical risk tranching, and strict solvency constraints. The protocol is designed to support protection-style markets (analogous to CDS and insurance) without relying on leverage, rehypothecation, or liquidation liquidity.

Rather than maximizing leverage, Siprifi maximizes *risk isolation, capital certainty, and settlement reliability* for binary and highly correlated assets.

---

## Motivation

Traditional protection markets (insurance, CDS, catastrophe bonds) suffer from persistent capital inefficiencies:

- Capital is locked in bilateral contracts for long durations  
- Risk transfer depends on the ongoing solvency of counterparties  
- Settlement often relies on discretionary or opaque processes  
- Capital buffers are fragmented and non-transparent  

Prediction markets solve price discovery for binary events but introduce new challenges:

- Binary payoff discontinuities  
- Extreme correlation during resolution  
- Liquidity evaporation near maturity  
- Incompatibility with mark-to-market liquidation models  

Siprifi addresses these limitations by combining prediction market primitives with **clearing house-style risk management**, enabling capital to be *structured rather than leveraged*.

---

## Core Design Principles

Siprifi is built on the following non-negotiable principles:

- **Pre-funded risk**  
  All losses are capitalized ex ante. The protocol never relies on future liquidity or forced liquidation.

- **Hierarchical risk tranching**  
  Every exposure has a clearly defined seniority and payment priority.

- **Binary-aware solvency modeling**  
  Risk is modeled assuming worst-case (100% VaR) outcomes for correlated binary assets.

- **No recursive leverage**  
  Capital may be reused only through explicit subordination, never through rehypothecation.

- **Deterministic settlement**  
  All contracts settle via protocol rules, not discretionary counterparties.

---

## What Siprifi Is

- A structured credit protocol for binary risk markets  
- A decentralized clearing layer for prediction-based exposures  
- A pre-funded protection market infrastructure  
- A solvency-first alternative to liquidation-driven DeFi systems  

---

## What Siprifi Is Not

- A lending or borrowing protocol  
- A leverage or yield amplification system  
- A traditional prediction market  
- An insurance protocol relying on under-collateralized promises  
- A system dependent on liquidators or secondary market liquidity  

---

## High-Level Architecture

Siprifi organizes risk into explicitly defined structures:

- **Senior Base Contracts**  
  Fully collateralized exposures backed by strong, non-binary assets (e.g. ETH, stablecoins). These define the maximum notional capacity of the system.

- **Subordinated Binary Credit Contracts**  
  Shorter-dated, conditional exposures backed by the non-occurrence of other events. These contracts are strictly subordinated and subject to correlation and duration constraints.

- **Protocol Solvency Buffers**  
  Explicit capital reserves designed to absorb tail-risk events and pricing errors.

- **Settlement Waterfall**  
  A deterministic payment hierarchy ensuring senior claims are never impaired by subordinated outcomes.

This architecture mirrors established financial systems such as CCP default funds, CDS tranching, and structured credit vehicles.

---

## Risk Management Model

Siprifi enforces solvency using conservative, worst-case assumptions:

- Binary assets are modeled with terminal values in \{0,1\}
- Correlated groups are defined by governance
- The largest correlated exposures are assumed to fail simultaneously
- Capital is reserved ex ante to absorb these failures

This ensures the protocol remains solvent even under extreme, discontinuous outcomes.

---

## Capital Efficiency (Without Leverage)

Siprifi improves capital efficiency not by increasing leverage, but by:

- Shortening contract duration where possible  
- Enforcing statistical decorrelation between exposures  
- Allowing subordinated risk to be issued only beneath senior collateral  
- Releasing capital deterministically at resolution  

Capital reuse occurs through **time, structure, and priority**, not through rehypothecation.

---

## Settlement and Solvency

All Siprifi contracts are settled through protocol-defined logic:

- No forced liquidations  
- No reliance on third-party liquidators  
- No assumptions of market liquidity at resolution  

Losses are absorbed according to a predefined waterfall, ensuring predictable and transparent outcomes for all participants.

---

## Repository Structure



## Repository Structure

```
siprifi/
├── README.md
├── docs/
│   ├── vision/
│   │   ├── siprifi_thesis.pdf
│   ├── protocol/
│   │   ├── SipUSD.md
│   │   ├── technical_whitepaper.md
│   │   ├── risk_management.md
|   |   |── Structured_credit_tranching_waterfall.md
|   |   |── Structured_Credit_for_Binary_Risk_Market.pdf
│   │   └── liquidation_and_oracles.md
│   ├── economics/
│   │   ├── CCP.md
│   │   ├── CDS.md
│   │   └── CLOs.md
│   ├── governance/
│   │   ├── governance_overview.md
│   │   └── risk_parameters.md
│   └── references/
│       ├── glossary.md
│       └── related_work.md
├── diagrams/
└── assets/
```

---

## Status

Siprifi is an active research and development project.  
Specifications are subject to change based on research, testing, and governance decisions.

This repository does not constitute an offer, solicitation, or financial advice.
---
