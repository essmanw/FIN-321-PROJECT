# Stage 5 – Final Analysis & Recommendation
**Author:** William Essman  
**Date:** December 2025  

---

## A. Exposure Summary
Our firm expects to **receive €17.8 million in one year** from an aircraft-component sale to a European customer.  

- **Timing:** 12 months (≈ 360 days)  
- **Spot rate (S₀):** 1.1600 USD/EUR  
- **Exposure:** ≈ USD $20.6 million at spot, fully unhedged  
- **Risk:** If the EUR depreciates (e.g., to 1.05 USD/EUR), USD receipts fall ≈ 9 %, threatening earnings stability and budget targets for FY 2026.  

The treasury objective is to lock in or stabilize USD cash flows while preserving liquidity and optionality.  

---

## B. Summary of Hedge Outcomes

| Strategy | Formula (USD Value) | Result (approx.) | Insight |
|-----------|--------------------|------------------|----------|
| **Forward Hedge** | € × 1.0935 | ≈ 19.46 m USD | Full certainty; no premium; locks rate ≈ –5.7 % below spot. |
| **Money-Market Hedge** | Borrow € /(1 + 3%) → convert @ 1.1600 → invest @ 4.75% | ≈ 19.45 m USD | Parity with forward; same economics; slightly more operational steps. |
| **EUR Put (1.1600)** | max(S_T, K_put) – premium (0.019) | ≈ 19.3 m @ EUR weak end; ≈ 20.6 m @ EUR strong end | Downside protected but premium reduces net USD. |
| **EUR Call (1.1600)** | S_T + max(S_T – K_call, 0) – premium (0.024) | ≈ 19.1–20.6 m USD range | Upside retained but adds cost and no downside floor. |

**Key Observation:** Forward and MM hedges produce nearly identical USD outcomes (consistent with covered interest parity). Options introduce cost but add flexibility to benefit from EUR strength.  

---

## C. Sensitivity Interpretation

| Scenario | EUR/USD change | Hedge Behavior | Insight |
|-----------|----------------|----------------|----------|
| **EUR depreciation (↓ 10 %)** | S_T ≈ 1.04 | Unhedged loses ≈ $1.9 m; Forward/MM fully protected; Put protects floor near 1.16 minus premium. | Forward/MM best for certainty; Put hedge costs premium but limits losses. |
| **EUR appreciation (↑ 10 %)** | S_T ≈ 1.28 | Unhedged and Call gain ≈ $1.9 m; Forward/MM capped at 19.45 m; Put underperforms because premium and no participation. | Call retains upside but is expensive; Forward/MM miss gains but remove uncertainty. |

**Interpretation:** The forward and money-market hedges offer certainty and perfect parity; option hedges provide strategic flexibility at a premium cost (~1.6–2.4 % of notional). For a firm prioritizing cash-flow stability over speculative upside, the forward remains most efficient.  

---

## D. Strategic Recommendation
**Recommended Hedge:** **Forward Contract (1-year @ 1.0935 USD/EUR)**  

**Rationale:**  
- Certainty of USD inflows (≈ $19.46 m) aligns with budget and reporting needs.  
- No up-front cash premium.  
- Consistent with interest-rate parity and risk-neutral valuation.  
- Money-market replicates the forward but requires borrowing and lending operations; less operationally efficient.  
- Options (put or collar) may be considered if management expects EUR strength or seeks strategic flexibility for partial hedging.  

---

## E. Executive Justification
- **Cash-Flow Stability:** Locks in budgeted USD receipts for FY 2026.  
- **Budget Certainty:** Simplifies forecasting and variance reporting.  
- **Liquidity:** Forward requires no up-front cash vs option premium outflows of ≈ $0.34–$0.43 m.  
- **Optionality:** Forgone in forward; acceptable given low likelihood of large EUR rally.  
- **Account**
