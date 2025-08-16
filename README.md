# Futura Tech — 10-Year Capital Budgeting Model for New Singapore Plant

## Visual Overview
<img width="1829" height="792" alt="image" src="https://github.com/user-attachments/assets/9165f370-1c98-4830-8b52-e7812e85f670" />

---

<img width="1758" height="454" alt="image" src="https://github.com/user-attachments/assets/e6e7b18e-6e7f-4b33-8582-1cf7a1093c97" />

---

<img width="1793" height="456" alt="image" src="https://github.com/user-attachments/assets/75db8cb9-835f-4943-8b3f-8532661a4cbc" />

---

<img width="1832" height="485" alt="image" src="https://github.com/user-attachments/assets/e7e453c3-9beb-4c26-a25b-b01ec36feaf9" />

---

<img width="1281" height="270" alt="image" src="https://github.com/user-attachments/assets/bbd7dda4-ca1b-4800-8acc-e3f538802399" />

---

## Case Description
Futura Tech Inc. (US-based, AI drones) evaluates building a manufacturing facility in Singapore. The model projects a 10-year plan with operating assumptions, PP&E roll-forward, working capital, financing, full P&L, operating cash flow, IRR, and invest/decline decision.

---

## Tasks
- Build a driver-based, auditable Excel model for a 10-year project.
- Roll forward PP&E from an initial capex program; compute straight-line D&A.
- Model DSO/DIO/DPO into Net Working Capital (NWC) and ΔNWC.
- Add a 10-year amortizing debt facility; compute interest via beginning-of-period debt.
- Produce P&L, Operating Cash Flow (unlevered), and residual value.
- Evaluate IRR vs. cost of capital and state the decision.

---

## Accounting/Analytics Steps (aligned to screenshots)

**1) Capex & PP&E roll-forward**
- Estimated initial investment: **$100m**; useful life **10 years**.
- Investment plan: **90% in Year 0**, **10% in Year 1**, then **2% each Year 2–10**.
- Straight-line D&A per vintage (start one year after spend). Example outputs:
  - D&A total by year (m): **Y1 −9.00, Y2 −10.00, …, Y10 −11.60**.
- Journal pattern each year:
  - Capex: `Dr PP&E` / `Cr Cash` (e.g., Y0: 90; Y1: 10; Y2–10: 2).
  - Depreciation: `Dr Depreciation Expense` / `Cr Accumulated Depreciation` (per schedule).

**2) Working Capital**
- Drivers provided: DSO declines **14→9**, DIO **88→79**, DPO **22→42** (Years 1–10).
- WC (m) example outputs: **Y1 −15.12 … Y10 −14.06**; ΔWC row ties to WC(t) − WC(t−1).

**3) Financing**
- Debt facility: **$80m**, **3%** rate, **10-year** amortization, equal total payment.
- Annual total payment ≈ **$9.38m**; repayments rise while interest falls:
  - Interest (m): **Y1 −2.40 → Y10 −0.27**.
  - Ending debt reaches **0** in Year 10.

**4) P&L**
- Variable expenses **75%** of revenue; fixed expenses **5%** of revenue.
- EBITDA margin therefore **20%**. Illustrative lines (m):
  - Revenue: **Y1 69.00 → Y10 111.54**
  - EBITDA: **Y1 13.80 → Y10 22.31**
  - EBIT = EBITDA − D&A; taxes at **30%** of EBT.

**5) Operating Cash Flow (unlevered)**
- OCF = **EBITDA − Taxes − ΔWC − Capex**; residual value at **Year 10: 15**.
- Example OCF (m): **Y0 −90.00; Y1 −12.04; …; Y10 18.10 (+15 residual)**.

---

## Trial Balance / Data Summary

**Key Inputs**
| Item | Value |
|---|---|
| Initial Capex | 100.0 |
| Life (years) | 10 |
| Capex timing | Y0 90%, Y1 10%, Y2–Y10 2% p.a. |
| Variable / Fixed costs | 75% / 5% of sales |
| Debt facility | 80 at 3%, amort. 10y |
| Tax rate | 30% |
| Residual value (Y10) | 15 |
| Discount rate (WACC) | 5.61% |
| IRR (project) | 6.79% |

**Checks**
- PP&E roll-forward: `Beg PP&E + Capex − D&A = End PP&E` (End(t) = Beg(t+1)).
- Debt roll-forward: `Beg Debt − Repayment = End Debt` (End(10) = 0).
- ΔWC row equals year-over-year change of WC.
- EBITDA margin constant at 20% (= 1 − 0.75 − 0.05).

---

## Financial Statements / Results

**Income Statement (selected years, $m)**  
| Year | Revenue | EBITDA | D&A | EBIT | Interest | EBT | Taxes (30%) | Net Income |
|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| 1 | 69.00 | 13.80 | (9.00) | **4.80** | (2.40) | 2.40 | (0.72) | **1.68** |
| 5 | 101.02 | 20.20 | (10.60) | **9.60** | (1.52) | 8.08 | (2.42) | **5.66** |
| 10 | 111.54 | 22.31 | (11.60) | **10.71** | (0.27) | 10.43 | (3.13) | **7.30** |

**Operating Cash Flow (headline)**  
- Sequence used for IRR: `[-90.00, -12.04, 11.81, 12.93, 13.41, 14.90, 16.54, 17.13, 17.74, 17.48, 18.10 + 15]`.  
- Result: **IRR 6.79% > WACC 5.61% → Accept the project.**

---

## Mapping / Logic (from drivers to outputs)

**PP&E / D&A**
- Annual D&A from each capex vintage: `Capex_k / Life`, recognized from `k+1` to `k+Life`.
- Total D&A in year *t*: `SUM over k≤t (Capex_k/Life)`.

**Working Capital**
- WC days: `CCC = DSO + DIO − DPO`.
- NWC: `Revenue_t × CCC_t / 365`.
- ΔWC_t: `NWC_t − NWC_{t−1}` (Y0 baseline = 0).

**Financing**
- Equal payment: `PMT = r * PV / (1 − (1+r)^−n)`.
- Interest_t: `BegDebt_t × r`; Repayment_t: `PMT − Interest_t`; EndDebt_t: `Beg − Repay`.

**Tax & Cash Flow**
- EBT_t: `EBIT_t − Interest_t`; Tax_t: `EBT_t × 30%`.
- OCF_t (unlevered): `EBITDA_t − Tax_t − ΔWC_t − Capex_t`.
- Residual value added in final year to OCF.

---

## How I Built It (Excel techniques & examples)

- Named ranges for drivers: `rev`, `dso`, `dio`, `dpo`, `capex`, `life`, `rate`, `tax`.
- **Depreciation grid** via `SUMPRODUCT` over capex vintages:
  ```excel
  =SUMPRODUCT(capex_range / life, --(col_year >= (row_vintage+1)))

## Debt schedule with built-ins:
Payment_t := PMT(rate, 10, -80)
Interest_t := IPMT(rate, t, 10, -80)
Principal_t := PPMT(rate, t, 10, -80)

## Working Capital
  ```excel
  =Revenue_t * ((DSO_t + DIO_t - DPO_t) / 365)
  =NWC_t - NWC_(t-1)   // ΔWC
```
## OCF & IRR:
  ```excel
  OCF_t := EBITDA_t - Tax_t - DeltaNWC_t - Capex_t
  =IRR(OCF_range)
```
## Quick Skills Snapshot
- Driver-based financial modeling (PP&E, WC, debt, taxes)
- Cash flow modeling & valuation (IRR, residual value, decision criteria)
- Excel modeling: PMT/IPMT/PPMT, SUMPRODUCT, named ranges, audit checks
- Statement linkage (P&L ↔ cash flow ↔ schedules) with roll-forward integrity
- Clear documentation and recruiter-ready presentation of results
