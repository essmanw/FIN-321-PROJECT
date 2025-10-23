# Executive Memo – FX Receivable Exposure (Scenario 4)

**Created by:** William Essman  
**Updated by:** William Essman  
**Date Created:** October 22 2025  
**Date Updated:** October 22 2025  
**Version:** 1.0  
**LLM Used:** GPT-5  

---

## Executive Summary (≤150 words)

Our firm, a U.S. aerospace manufacturer, expects to receive **€17.8 million** in **one year**, representing a **USD $20 million** receivable at today’s EUR/USD spot of **1.1600**. Because the dollar value we ultimately collect depends on the **EUR/USD exchange rate**, any euro depreciation would reduce our proceeds in USD. The **one-year forward rate = 1.0935** implies market expectations for a weaker euro. With interest rates near **USD 4.75 %** and **EUR 3.00 %**, we recommend evaluating a hedge strategy to stabilize future cash inflows and protect budget certainty.

---

## Background & Objectives

This exposure arises from European customer contracts denominated in euros but accounted for in dollars. If the **EUR** falls against the **USD**, the same euro amount converts to fewer dollars, reducing revenue.  
Our objective is to design an FX risk-management framework that protects our USD cash flow while balancing cost, flexibility, and potential upside participation.

---

## Methods

We will assess three hedge families:

1. **Forward Contract** – Locks a fixed EUR/USD = 1.0935.  
   *Pros:* Eliminates uncertainty; simple to execute.  
   *Cons:* No upside if EUR strengthens; marks-to-market until maturity.

2. **Money-Market Hedge** – Borrow EUR / invest USD at current rates (EUR ≈ 3.00 %, USD ≈ 4.75 %).  
   *Pros:* Replicates a synthetic forward; no option premium.  
   *Cons:* Requires balance-sheet capacity; accounting complexity.

3. **Option Hedge** – Buy a **put on EUR (k = 1.1600, premium = $0.019)** and/or sell a **call on EUR (k = 1.1600, premium = $0.024)**.  
   *Pros:* Downside protection with potential upside retention.  
   *Cons:* Premium cost; strike-selection trade-offs.

---

## Limitations & Next Steps

Assumptions rely on current market quotes and indicative rates. Actual executable pricing may vary with notional size and counterparty credit.  
Next, we will:

1. **Stage 2–3:** Build a quantitative Excel model to compare hedge payoffs under multiple EUR/USD scenarios.  
2. Develop a **prompt specification** enabling an AI agent to automate spreadsheet generation from inputs (spot, forward, rates, and premiums).  
3. Provide a **final recommendation** quantifying net USD outcomes and hedge efficiency.

---

## References

- Bloomberg Markets (2025). EUR/USD Spot 1.1600, Forward 1Y 1.0935.  
- Federal Reserve & ECB policy rates as of October 2025 (USD ≈ 4.75 %, EUR ≈ 3.00 %).  
- Corporate Finance Institute – FX Hedging Methods (2024).  
