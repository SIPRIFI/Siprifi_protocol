<p align="center">
  <img src="../../assets/siprifi-logo.png" alt="Siprifi Logo" width="600">
</p>

# sipUSD — Technical Definition and Economic Role

## 1. One-Sentence Definition

**sipUSD is a non-redeemable, floating-NAV equity unit that represents a proportional claim on the protocol’s total loss-absorbing capacity, similar to the equity layer of a Central Counterparty (CCP).**

In short:

> **sipUSD is equity, not money.**

---

## 2. What sipUSD Is (and Is Not)

### What sipUSD **IS**
- A **residual equity unit**
- **Loss-absorbing** by design
- **Supply-elastic**
- Priced by **system NAV**, not a peg
- Backed by **risk capacity**, not promises
- Subordinate to all protection buyers

### What sipUSD **IS NOT**
- ❌ A stablecoin  
- ❌ Redeemable for $1  
- ❌ Debt or IOU  
- ❌ Fully backed by reserves  
- ❌ Guaranteed purchasing power  

---

## 3. Why sipUSD Resembles a Central Counterparty (CCP) Equity Layer

In traditional finance, a **Central Counterparty (CCP)** manages counterparty risk using a layered default waterfall.

### CCP Risk Waterfall (TradFi)

| Layer | Description |
|----|----|
| 1 | Member margin (first loss) |
| 2 | Default fund |
| 3 | CCP equity (“skin in the game”) |
| 4 | Mutualized loss allocation |

The **equity layer**:
- Is **not redeemable**
- Absorbs losses before seniors
- Gains value when defaults do *not* occur
- Shrinks when correlated failures happen

👉 **sipUSD plays exactly this role — on-chain, for binary risk.**

---

## 4. sipUSD in Siprifi’s Risk Waterfall

| Layer | Instrument | Role |
|----|----|----|
| Senior | Strong collateral (ETH / USDC) | Final backstop |
| Mezzanine | Protocol buffers / fees | Shock absorber |
| Junior | EBP-qualified NO exposure | First loss |
| **Equity** | **sipUSD** | Residual loss-absorbing unit |

sipUSD holders sit **below all protection buyers** and above nothing.

---

## 5. What Backs sipUSD (NAV Components)

sipUSD is backed **only** by assets that can absorb losses under protocol rules.

### Included in NAV

| Component | Description |
|----|----|
| \(A_{res}\) | Strong collateral (ETH / USDC) |
| \(V_{NO}^{EBP}\) | EBP-qualified NO exposure (discounted, correlated, duration-adjusted) |
| \(F_{protocol}\) | Protocol-retained fees / buffers |

### Excluded from NAV

| Excluded Item | Reason |
|----|----|
| YES tokens | Upside claims, not loss-absorbing |
| Raw premiums | Not protocol equity |
| Expected value | NAV prices downside only |
| Market prices | NAV uses worst-case valuation |

---

## 6. NAV Formula (Siprifi-Accurate)

$$
NAV_{sys}
=
\frac{
A_{res}
+
V_{NO}^{EBP}
+
F_{protocol}
-
L_{sys}
}{
S_{sipUSD}
}
$$

Where:

- $A_{res}$ = senior collateral reserves  
- $V_{NO}^{EBP}$ = loss-absorbing NO exposure after SCE constraints  
- $F_{protocol}$ = protocol-owned buffers  
- $L_{sys}$ = system-level obligations  
- $S_{sipUSD}$ = total sipUSD supply  

---

## 7. Why sipUSD Has a “Price” Without a Peg

sipUSD does **not** promise redemption.

Its **fair value** is:

\[
Price_{sipUSD} \approx NAV_{sys}
\]

Market prices may deviate, but:
- **Minting**
- **Risk limits**
- **Deleveraging**
- **Dilution**

All operate strictly on **NAV**, not market price.

---

## 8. Numerical Example

### Initial State

| Item | Value |
|----|----|
| Loss-absorbing capacity | \$1,000,000 |
| sipUSD supply | 1,000,000 |
| **NAV** | **1.00** |

### After Adverse Event

- Correlated events consume \$300,000 of NO capacity

| Item | Value |
|----|----|
| Remaining capacity | \$700,000 |
| sipUSD supply | 1,000,000 |
| **NAV** | **0.70** |

➡ sipUSD did **not fail**  
➡ sipUSD **absorbed the loss**

This is correct behavior.

---

## 9. Comparison Table

| Instrument | Redeemable | Pegged | Loss-Absorbing | Equity-Like |
|----|----|----|----|----|
| Stablecoin | ✅ | ✅ | ❌ | ❌ |
| DAI | Partial | Soft | Indirect | ❌ |
| MKR | ❌ | ❌ | ✅ | ✅ |
| CCP Equity | ❌ | ❌ | ✅ | ✅ |
| **sipUSD** | ❌ | ❌ | ✅ | ✅ |

---

## 10. Final Interpretation

> **sipUSD is the equity layer of an on-chain structured credit and protection system, priced by NAV and designed to absorb binary risk rather than eliminate it.**

It does not try to make risk disappear.  
It **prices it honestly**.
