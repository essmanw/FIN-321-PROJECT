# Deliverable 1 — Structured AI Prompt (Executable)

**Role:** Finance Technologist / Treasury Analyst — build a complete, professional **Excel** model for a EUR receivable hedge using the instructions below. Generate the spreadsheet, formulas, named ranges, color rules, cross-checks, and export a downloadable `.xlsx` file.

---

## A) Scenario-Specific Variables (use these exact values)

- **FC_AMT** (EUR receivable): **€17,800,000**
- **S0_in** (spot EUR/USD, USD per EUR, looked up on **December 09, 2025**): **1.1637**
  - Source hint: ECB euro reference rate (daily).
- **F0_in** (1Y forward rate, provided): **1.0935**
- **R_USD** (USD 1Y rate, simple p.a., looked up): **4.00%**
  - Source hint: Federal Funds Target Range — Upper Limit.
- **R_FC** (EUR 1Y rate, simple p.a., looked up): **2.00%**
  - Source hint: ECB **deposit facility** rate.
- **K_PUT** (EUR put strike): **1.1600**
- **K_CALL** (EUR call strike): **1.1600**
- **PREM_PUT** (put premium, USD per EUR): **0.019**
- **PREM_CALL** (call premium, USD per EUR): **0.024**
- **T_DAYS**: **365**
- **T_YRS**: compute as `=T_DAYS/365` (no leap-year adjustment)

> Notes: Option premiums are paid upfront in USD. Exchange rates are USD per EUR. Hedge notional equals the full receivable. Maturity is 1 year.

---

## B) Excel Build Requirements

### 1) Named Ranges (create exactly these)
`FC_AMT, S0_in, F0_in, R_USD, R_FC, K_PUT, K_CALL, PREM_PUT, PREM_CALL, T_DAYS, T_YRS`

### 2) Color Coding (cell fill)
- **Yellow** = *Inputs / decision variables* (all named ranges above)
- **Blue** = *Assumptions* (conventions, date stamps, units)
- **Green** = *Formulas / intermediate calcs*
- **Gray** = *Outputs / KPIs*

### 3) Model Components (implement and label sections)

**(a) Forward Hedge**
- USD proceeds at maturity: `USD_forward = FC_AMT * F0_in`

**(b) Money Market Hedge (3-step)**
1. EUR to borrow now: `EUR_borrow = FC_AMT / (1 + R_FC * T_YRS)`  
2. Convert at spot and invest in USD: `USD_invest = EUR_borrow * S0_in`  
3. Maturity USD: `USD_mm = USD_invest * (1 + R_USD * T_YRS)`  

**(c) Option Hedges (premium + payoff)**
- Define a *scenario spot at maturity* `S_T` (a green formula driver).
- EUR **put** payoff per EUR at *maturity*: `put_payoff_per_EUR = MAX(K_PUT - S_T, 0)`  
  - Total: `PUT_payoff = FC_AMT * put_payoff_per_EUR`  
  - Net USD receipts from receivable + option: `USD_put = FC_AMT * S_T + PUT_payoff - FC_AMT * PREM_PUT`
- EUR **call** payoff per EUR at *maturity*: `call_payoff_per_EUR = MAX(S_T - K_CALL, 0)`  
  - Total: `CALL_payoff = FC_AMT * call_payoff_per_EUR`  
  - Net USD receipts: `USD_call = FC_AMT * S_T - FC_AMT * PREM_CALL + CALL_payoff`

**(d) Unhedged Benchmark**
- `USD_unhedged = FC_AMT * S_T`

**(e) Sensitivity Table**
- Two-way or one-way table across **S_T ∈ [0.95×S0_in, 1.05×S0_in]** in 0.01 increments (1-cent in USD/EUR).  
- Columns: `S_T`, `USD_forward`, `USD_mm`, `USD_put`, `USD_call`, `USD_unhedged`.
- Add a chart “**Hedge Payoffs vs S_T**” plotting each series.

**(f) Formatting & Documentation**
- Put an *Inputs* panel at the top (yellow), a compact *Assumptions* block (blue), *Calculations* (green), and *Outputs/KPIs* (gray).  
- Display key KPIs: locked-in USD from forward, USD from MM hedge, expected option outcomes at S_T = S0_in, and range statistics (min/max across the sensitivity).

### 4) Cross‑Checks & Parity
- **Interest‑rate parity**: compute `F_theoretical = S0_in * (1 + R_USD*T_YRS) / (1 + R_FC*T_YRS)` and show `ΔF = F0_in - F_theoretical` (gray).  
- **Consistency**: check `ABS(USD_forward - USD_mm) < 0.01 * USD_forward` and flag PASS/FAIL.  
- **Named-range audit**: list all named ranges with `=NAME.MANAGER()` equivalent output or a generated mapping table.

---

## C) Verification & Delivery Instructions (the AI must perform these)
1. **Validate parity**: Report `F_theoretical`, `ΔF`, and PASS/FAIL of `USD_forward` ≈ `USD_mm` test.  
2. **Confirm named ranges**: Return a table with each required name, scope, and cell address.  
3. **Return full formula mapping**: For each output/KPI and key intermediate (items above), output the exact Excel formula text and the dependent named ranges.  
4. **Provide artifact**: Produce and return a **downloadable `.xlsx` file** with the build, the sensitivity table, and the chart.

---

## D) Implementation Hints (non-binding but recommended)
- Use simple (non-annualized) interest over `T_YRS` as specified.  
- Keep units explicit (USD per EUR).  
- Place a date-stamp cell with today’s date `2025-12-09` and freeze panes for usability.  
- Use consistent number formats: 4 decimals for FX rates, 2 for USD amounts, percentages for rates.

---

## Source Context (for the AI, not for the CFO)
This prompt is derived from our Stage 2 specification (variables, flow, and outputs) and implements the Stage 3 logic described therein.
