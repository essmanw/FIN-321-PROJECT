# Technical Specification – FX Receivable Hedge Analysis (Scenario 4)

**Created by:** William Essman  
**Updated by:** William Essman  
**Date Created:** October 22 2025  
**Date Updated:** October 22 2025  
**Version:** 1.1  


**Role:** Financial Analyst / Treasury Analyst  
**Audience:** CFO or Director of Treasury  

**Purpose:** Quantitatively outline the framework and structure for analyzing alternative FX-hedging strategies for a EUR-denominated receivable due in one year. The specification defines variables, assumptions, analytical flow, and outputs that will feed the Stage 3 Excel model and later AI-prompt generation.


## 1. Problem Statement

Our company, a U.S. aerospace manufacturer, will receive €17.8 million in one year (≈ USD $20 million at spot 1.1600). Because our financial reporting is in USD, we face exposure to EUR/USD depreciation risk. The objective is to evaluate and compare hedging alternatives that stabilize USD proceeds while balancing cost and flexibility.  
This specification supports the treasury decision on whether and how to hedge the exposure through forwards, money-market instruments, or options.


## 2. Inputs (Known Variables)

| Variable | Description | Unit | Example Value | Source |
|-----------|-------------|------|---------------|--------|
| `FC_AMT` | Foreign-currency receivable | EUR | 17,800,000 | Company data |
| `S₀` | Current EUR/USD spot rate | USD per EUR | 1.1600 | Market data (Oct 22 2025) |
| `F₀` | 1-year EUR/USD forward rate | USD per EUR | 1.0935 | Provided scenario |
| `r_USD` | USD 1-year interest rate | % p.a. | 4.75 % | Market data |
| `r_EUR` | EUR 1-year interest rate | % p.a. | 3.00 % | Market data |
| `t` | Time to maturity | Years | 1 | Derived |
| `K_put` | EUR put strike price | USD per EUR | 1.1600 | Set at spot |
| `K_call` | EUR call strike price | USD per EUR | 1.1600 | Set at spot |
| `Premium_put` | Put premium | USD per EUR | 0.019 | Scenario |
| `Premium_call` | Call premium | USD per EUR | 0.024 | Scenario |


## 3. Assumptions & Constraints

- Interest rates are annualized on a simple-compounding basis.  
- Forward rate represents a 1-year maturity quotation.  
- Transaction costs, margin requirements, and counterparty credit risk are excluded.  
- Option premiums are paid upfront in USD.  
- Exchange rates are quoted as USD per EUR.  
- Hedge notionals match the full receivable notional (€17.8 m).  
- All instruments settle in one year (t = 1).  


## 4. Calculation Flow

1. **Forward Hedge** – Compute locked-in USD proceeds: `EUR × F₀`.  
2. **Money-Market Hedge** – Borrow EUR today at r_EUR, convert to USD at spot S₀, and invest at r_USD; confirm parity with F₀.  
3. **Option Hedge** – Model payoffs at maturity S_T:  
   - EUR Put (k = 1.1600): `max(K_put − S_T, 0)` × EUR − premium.  
   - EUR Call (k = 1.1600): `max(S_T − K_call, 0)` × EUR − premium.  
4. **Unhedged Case** – Benchmark: `EUR × S_T`.  
5. **Scenario Analysis** – Vary S_T across plausible EUR/USD paths.  
6. **Compare Outcomes** – Summarize USD results, highlight certainty, optionality, and cost.  

## 5. Outputs

| Output | Description | Format | Purpose |
|---------|--------------|---------|----------|
| `USD_forward` | USD value of forward hedge | Numeric | Certainty benchmark |
| `USD_mm` | USD value from money-market hedge | Numeric | Cross-check against forward |
| `USD_put` | USD receipts under EUR put | Table | Downside protection analysis |
| `USD_call` | USD receipts under EUR call | Table | Upside participation case |
| `Chart_1` | Hedge payoffs vs. spot at maturity | Line chart | Visual comparison |
| `Summary` | Written takeaway of hedge trade-offs | Text | Executive decision support |


## 6. Sensitivity Plan

Vary EUR/USD spot at maturity \(S_T\) from 0.95 × S₀ = 1.10 to 1.05 × S₀ = 1.22 in increments of 0.01.  
For each S_T, compute USD receipts under forward, money-market, put, call, and unhedged positions.  
Present results as a comparison table and plot all hedges on one chart to illustrate certainty vs. optional value.


## 7. Limitations & Next Steps

This specification excludes implied volatility, premium discounting, and transaction costs. All inputs reflect current indicative market data.  
The next step (Stage 3) is to build the Excel model implementing this logic to quantify USD outcomes under each hedge and to develop the AI prompt that automates spreadsheet creation from these inputs.


## References

- Bloomberg Markets (2025). EUR/USD Spot 1.1600, Forward 1Y 1.0935.  
- Federal Reserve & European Central Bank policy rates (USD ≈ 4.75 %, EUR ≈ 3.00 %).  
- Corporate Finance Institute (2024). “FX Hedging Methods and Model Construction.”  

