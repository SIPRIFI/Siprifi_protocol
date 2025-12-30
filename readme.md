# Siprifi Finance

Siprifi Finance is a decentralized protocol that turns prediction market outcome shares into productive collateral, enabling capital-efficient protection markets and reusable liquidity.

By combining prediction-based risk primitives with a DeFi-native lending layer, Siprifi allows risk to be priced, traded, collateralized, and redeployed across uncorrelated exposures.

---

## Motivation

Traditional protection markets (such as insurance and CDS) suffer from structural capital inefficiencies:

- Capital is locked in bilateral contracts for long durations  
- Liquidity is one-sided and disappears during periods of stress  
- Risk transfer depends on the continuous willingness of protection sellers  

Prediction markets solve price discovery but still suffer from siloed capital: funds committed to a single market cannot be reused elsewhere.

Siprifi addresses this limitation by enabling prediction market outcome shares to function as collateral in a lending protocol, unlocking capital while preserving over-collateralization and protocol solvency.

---

## High-Level Design

Siprifi is built on a modified Aave-style lending architecture and introduces several key innovations:

- Prediction market YES/NO shares as collateral  
- Over-collateralized borrowing against outcome shares  
- Governance-defined correlated risk groups  
- Borrowing power adjusted for concentration and correlation risk  
- Standard DeFi liquidations and oracle-based pricing  

This design allows users to reuse capital across multiple uncorrelated risks while preventing excessive leverage on concentrated or correlated outcomes.

---

## What Siprifi Is (and Is Not)

**Siprifi is:**
- A lending protocol for prediction market assets  
- A capital efficiency layer for protection markets  
- A DeFi-native risk management system  

**Siprifi is not:**
- A prediction market itself  
- A traditional insurance protocol  
- An uncollateralized risk-sharing system  

---

## Documentation

The repository is organized into conceptual, technical, and economic documents:

- **Technical Whitepaper**  
  `docs/protocol/technical_whitepaper.md`  
  Formal specification of protocol mechanics, risk parameters, and liquidation logic.

- **Siprifi Thesis**  
  `docs/vision/siprifi_thesis.md`  
  Conceptual and economic rationale for market-based protection systems.

- **Protocol Overview**  
  `docs/protocol/protocol_overview.md`  
  High-level architecture and user flows.

- **Risk Management**  
  `docs/protocol/risk_management.md`  
  Detailed explanation of diversification rules and correlated risk handling.

See the full document map in the repository structure section below.

---

## Repository Structure

```
siprifi/
├── README.md
├── docs/
│   ├── vision/
│   │   ├── siprifi_thesis.pdf
│   ├── protocol/
│   │   ├── protocol_overview.md
│   │   ├── technical_whitepaper.md
│   │   ├── risk_management.md
│   │   └── liquidation_and_oracles.md
│   ├── economics/
│   │   ├── protection_markets.md
│   │   ├── capital_efficiency.md
│   │   └── market_dynamics.md
│   ├── governance/
│   │   ├── governance_overview.md
│   │   └── risk_parameters.md
│   └── references/
│       ├── glossary.md
│       └── related_work.md
├── contracts/
├── diagrams/
└── assets/
```

---

## Status

Siprifi is an active research and development project.  
Specifications are subject to change based on research, testing, and governance decisions.

This repository does not constitute an offer, solicitation, or financial advice.

---

## License

(Add license information here)
