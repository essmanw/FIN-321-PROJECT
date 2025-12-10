You are a financial modeling assistant acting as a **Finance Technologist / Treasury Analyst**. Build an auditable Excel model for hedging a EUR receivable using forwards, a 3-step money-market hedge, and options.

# GOAL
Generate a clean, professional `.xlsx` that computes and compares USD proceeds for forward, money-market, and option hedges on a EUR receivable, with sensitivity analysis and verification checks.

# CONTEXT
This prompt implements Scenario 4 from my Stage 2 specification and follows the logic in my Stage 3 workbook. Use the exact variable names and structure below — do not invent new names. Keep exchange-rate quotes as **USD per EUR**.

# INPUT VARIABLES (explicit values)
FC_AMT = 17,800,000  
S0_in = 1.1600  
F0_in = 1.0935  
R_USD = 0.0475            # 4.75% p.a.  
R_FC  = 0.0300            # 3.00% p.a.  
K_PUT = 1.1600  
K_CALL = 1.1600  
PREM_PUT = 0.019          # USD per EUR, paid upfront  
PREM_CALL = 0.024         # USD per EUR, paid upfront  
T_DAYS = 360  
T_YRS  = T_DAYS/360       # derive in-sheet

# SPREADSHEET REQUIREMENTS
1) **Named Ranges (exact names):**  
`FC_AMT, S0_in, F0_in, R_USD, R_FC, K_PUT, K_CALL, PREM_PUT, PREM_CALL, T_DAYS, T_YRS`

2) **Color Coding (strict):**  
- Yellow = Inputs / decision variables (`FC_AMT, S0_in, K_PUT, K_CALL, PREM_PUT, PREM_CALL, T_DAYS`)  
- Blue = Assumptions (`F0_in, R_USD, R_FC`)  
- Green = Formulas  
- Gray  = Outputs / KPIs

3) **Model Components & Layout (labeled sections):**  
- **Forward Hedge:** `USD_forward = FC_AMT × F0_in`.  
- **Money-Market Hedge (3-step):**  
  1. EUR borrowed today: `EUR_borrow = FC_AMT / (1 + R_FC × T_YRS)`  
  2. USD today: `USD_today = EUR_borrow × S0_in`  
  3. USD at maturity: `USD_mm = USD_today × (1 + R_USD × T_YRS)`  
- **Covered Interest Parity (CIP) cross-check:**  
  `F_implied = S0_in × (1 + R_USD × T_YRS) / (1 + R_FC × T_YRS)` and report `(F_implied − F0_in)/F0_in` in bps.  
- **Options (premium + payoff):** with spot at maturity `S_T`  
  - Unhedged: `USD_unhedged = FC_AMT × S_T`  
  - Long EUR Put: `USD_put = FC_AMT × max(S_T, K_PUT) − PREM_PUT × FC_AMT`  
  - Long EUR Call: `USD_call = FC_AMT × (S_T + max(S_T − K_CALL, 0)) − PREM_CALL × FC_AMT`  
- **Sensitivity Table:** vary `S_T` from `0.95×S0_in` to `1.05×S0_in` in 0.01 increments and compute `USD_unhedged, USD_put, USD_call, USD_forward, USD_mm`.  
- **Outputs / KPIs (Gray):** `USD_forward, USD_mm, CIP_diff_bps`.

4) **Formatting**
- Clear section headers, consistent number formats, freeze panes, and a separate **Sensitivity** sheet.
- Provide an **Audit** sheet listing each named range and its absolute cell reference.

# NAMED RANGE DEFINITIONS
Create workbook-level names exactly as listed under “Named Ranges”. Use them in all formulas and sensitivity logic.

# MODEL LOGIC (PSEUDOCODE)
