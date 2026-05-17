---
template: spec
purpose: "Technical specification for the Apple Inc. (AAPL) accounting & performance ratios model — defines scope, inputs, formulas, validation, and analysis requirements precisely enough that any competent executor (human or LLM) can reconstruct the Excel model and produce a correct, comprehensive financial analysis"
audience: student
fields_required: [title, author, date, version, company, scope, model_architecture, data_inputs, derived_inputs, formulas, validation, analysis_requirements, output_format, references]
naming_convention: "YYYY-MM-DD-{slug}.md"
courses: [BUS-629]
notes: "Stage 4 deliverable for BUS-629. Source model: models/builds/2026-05-16-pham-apple-financials.xlsx. Named-range suffix convention is _curr / _prior (not _YYYY)."
---

# Accounting & Performance Ratios Analysis — Apple Inc.

**Author:** Truc Pham
**Date:** 2026-05-17
**Version:** 1.0
**Company:** Apple Inc., AAPL, NASDAQ

---

## 1. Scope & Objective

This specification defines a complete accounting-ratios model for **Apple Inc. (NASDAQ: AAPL)** and the financial analysis it must produce.

- **Fiscal period:** FY2025 (52-week year ended Sep 27, 2025), with FY2024 (ended Sep 28, 2024) as the prior/start-of-year comparative.
- **Reporting standard:** US GAAP.
- **Reporting currency / units:** USD millions (per-share figures in USD; share counts in millions).
- **Source filing:** Apple Inc. Form 10-K, SEC EDGAR (CIK 0000320193), filed Oct 31, 2025; auditor Ernst & Young LLP, unqualified opinion.
- **Analytical objective:** Compute ~30 performance, profitability, efficiency, leverage, and liquidity ratios from a three-statement model, decompose ROE via the Du Pont system, and deliver an evidence-based assessment of Apple's financial condition with 3–5 strategic recommendations.
- **Intended audience for the output:** A finance-literate reader (instructor / investment committee) who wants a defensible diagnostic of Apple's returns, capital structure, and liquidity, not a tutorial.

An executor reading this spec must reproduce the model **without looking up, inferring, or estimating any figure** — every input is stated numerically in Section 3.

---

## Part A — Model Specification

### 2. Model Architecture

The workbook contains **six tabs**; data flows left-to-right from statements → derived inputs → ratio outputs.

| Tab | Role | Contents |
|-----|------|----------|
| **Cover** | Reference | Usage instructions, color key, named-range convention. |
| **Balance Sheet** | Input | FY current + FY prior, two-sided (Assets ‖ Liabilities & Equity). Subtotals are formulas. |
| **Income Statement** | Input | FY current only; EBIT, taxable income, net income, RE allocation are formulas; column D = % of sales. |
| **Cash Flow Statement** | Input | FY current; operations references `INC_*`; investing/financing entered; subtotals are formulas. |
| **Ratios** | Calculation + Output | Four analyst assumptions + derived inputs (rows 6–38); ratio outputs (rows 41–76). |
| **Notes** | Reference | Company metadata, data source, reporting standard, statement reclassifications, self-checks. |

**Color / formatting conventions:**
- **Yellow background** — DATA INPUTS (figures from the 10-K). Overwrite per company.
- **Light-blue background + blue text** — ASSUMPTIONS (share price, shares outstanding, WACC, tax rate, fiscal years).
- **Green text** — FORMULAS (cross-sheet references, derived calculations). Do not overwrite.
- **Gray background** — RATIO OUTPUTS (computed in the Ratios tab). Do not overwrite.

**Input / calculation / output separation:** raw 10-K figures live only on the three statement tabs; every derived value and ratio on the Ratios tab is a formula referencing **named ranges**, never raw cell addresses.

**Named-range convention** (suffix is `_curr` / `_prior`, *not* `_YYYY`):
- `BAL_[item]_curr` / `BAL_[item]_prior` — balance-sheet line items.
- `INC_[item]` — income-statement items (current year).
- `CASH_[item]` — cash-flow items.
- `share_price`, `shares_outstanding`, `cost_capital`, `tax_rate` — analyst assumptions (no prefix).
- `startYear_[item]` — alias for prior-year balance; `currentYear_[item]` — current-year balance or derived figure.
- `avg_[item]` — mean of start-of-year and current-year.
- `RATIO_[name]` — the four ratios reused in Du Pont (`asset_turnover`, `operating_profit_margin`, `leverage`, `debt_burden`).

### 3. Data Inputs

All values in **USD millions** unless noted. FY current = FY2025; FY prior = FY2024. Subtotals marked *(formula)* are computed, not entered — listed for completeness.

**Balance Sheet — Assets**

| Named Range | Source | Value (curr) | Value (prior) | Unit |
|-------------|--------|-------------:|--------------:|------|
| `BAL_cash_marketable_securities_curr` / `_prior` | Balance Sheet | 54,697 | 65,171 | $M |
| `BAL_receivables_curr` / `_prior` | Balance Sheet | 72,957 | 66,243 | $M |
| `BAL_inventories_curr` / `_prior` | Balance Sheet | 5,718 | 7,286 | $M |
| `BAL_other_current_assets_curr` / `_prior` | Balance Sheet | 14,585 | 14,287 | $M |
| `BAL_assets_current_curr` / `_prior` *(formula)* | Balance Sheet | 147,957 | 152,987 | $M |
| `BAL_ppe_gross_curr` / `_prior` | Balance Sheet | 49,834 | 45,680 | $M |
| `BAL_accumulated_depreciation_curr` / `_prior` | Balance Sheet | 0 | 0 | $M |
| `BAL_fixed_assets_net_curr` / `_prior` *(formula)* | Balance Sheet | 49,834 | 45,680 | $M |
| `BAL_intangibles_curr` / `_prior` | Balance Sheet | 0 | 0 | $M |
| `BAL_other_assets_curr` / `_prior` | Balance Sheet | 161,450 | 166,313 | $M |
| `BAL_assets_total_curr` / `_prior` *(formula)* | Balance Sheet | 359,241 | 364,980 | $M |

**Balance Sheet — Liabilities & Equity**

| Named Range | Source | Value (curr) | Value (prior) | Unit |
|-------------|--------|-------------:|--------------:|------|
| `BAL_debt_short_term_curr` / `_prior` | Balance Sheet | 20,329 | 20,879 | $M |
| `BAL_accounts_payable_curr` / `_prior` | Balance Sheet | 69,860 | 68,960 | $M |
| `BAL_other_current_liabilities_curr` / `_prior` | Balance Sheet | 75,442 | 86,553 | $M |
| `BAL_liabilities_current_curr` / `_prior` *(formula)* | Balance Sheet | 165,631 | 176,392 | $M |
| `BAL_debt_long_term_curr` / `_prior` | Balance Sheet | 78,328 | 85,750 | $M |
| `BAL_other_long_term_liabilities_curr` / `_prior` | Balance Sheet | 41,549 | 45,888 | $M |
| `BAL_liabilities_total_curr` / `_prior` *(formula)* | Balance Sheet | 285,508 | 308,030 | $M |
| `BAL_common_stock_curr` / `_prior` | Balance Sheet | 93,568 | 83,276 | $M |
| `BAL_retained_earnings_curr` / `_prior` | Balance Sheet | −19,835 | −26,326 | $M |
| `BAL_equity_shareholders_curr` / `_prior` *(formula)* | Balance Sheet | 73,733 | 56,950 | $M |

**Income Statement (FY2025)**

| Named Range | Source | Value | Unit |
|-------------|--------|------:|------|
| `INC_sales` | Income Statement | 416,161 | $M |
| `INC_cost_goods_sold` | Income Statement | 220,960 | $M |
| `INC_sga` | Income Statement | 50,453 | $M |
| `INC_depreciation` | Income Statement | 11,698 | $M |
| `INC_ebit` *(formula)* | Income Statement | 133,050 | $M |
| `INC_other_income` | Income Statement | −321 | $M |
| `INC_interest_expense` | Income Statement | 0 | $M |
| `INC_taxable_income` *(formula)* | Income Statement | 132,729 | $M |
| `INC_taxes` | Income Statement | 20,719 | $M |
| `INC_net` *(formula)* | Income Statement | 112,010 | $M |
| `INC_dividends` | Income Statement | 15,421 | $M |
| `INC_addition_retained_earnings` *(formula)* | Income Statement | 96,589 | $M |

**Cash Flow Statement (FY2025)**

| Named Range | Source | Value | Unit |
|-------------|--------|------:|------|
| `CASH_operating` *(= net income + dep + Δworking capital)* | Cash Flow | 111,482 | $M |
| `CASH_investments` *(formula, sum of investing)* | Cash Flow | 15,195 | $M |

**Analyst Assumptions (Ratios tab)**

| Named Range | Source | Value | Unit |
|-------------|--------|------:|------|
| `yearCurrent` | Analyst input | 2025 | year |
| `yearStart` *(= yearCurrent − 1)* | Analyst input | 2024 | year |
| `share_price` | Market data (FY2025 close) | 255.46 | USD |
| `shares_outstanding` | Market data | 14,773.26 | M shares |
| `cost_capital` | Analyst assumption | 0.085 | decimal |
| `tax_rate` | Analyst assumption | 0.156 | decimal |

### 4. Derived Inputs

Computed on the Ratios tab from named ranges. Formulas in named-range notation; values shown for verification.

| Named Range | Formula | Value |
|-------------|---------|------:|
| `market_capitalization` | `share_price × shares_outstanding` | 3,773,977 |
| `startYear_equity` | `BAL_equity_shareholders_prior` | 56,950 |
| `startYear_inventory` | `BAL_inventories_prior` | 7,286 |
| `startYear_receivables` | `BAL_receivables_prior` | 66,243 |
| `startYear_total_assets` | `BAL_assets_total_prior` | 364,980 |
| `startYear_total_capitalization` | `BAL_debt_long_term_prior + BAL_equity_shareholders_prior` | 142,700 |
| `currentYear_after_tax_operating_income` | `INC_net + (1 − tax_rate) × INC_interest_expense` | 112,010 |
| `currentYear_daily_sales_average` | `INC_sales / 365` | 1,140.17 |
| `currentYear_equity` | `BAL_equity_shareholders_curr` | 73,733 |
| `currentYear_cash_marketable_securities` | `BAL_cash_marketable_securities_curr` | 54,697 |
| `currentYear_assets_current` | `BAL_assets_current_curr` | 147,957 |
| `currentYear_liabilities_current` | `BAL_liabilities_current_curr` | 165,631 |
| `currentYear_cost_goods_sold_daily` | `INC_cost_goods_sold / 365` | 605.37 |
| `currentYear_debt_long_term` | `BAL_debt_long_term_curr` | 78,328 |
| `currentYear_working_capital_net` | `BAL_assets_current_curr − BAL_liabilities_current_curr` | −17,674 |
| `currentYear_assets_total` | `BAL_assets_total_curr` | 359,241 |
| `currentYear_total_capitalization` | `currentYear_debt_long_term + currentYear_equity` | 152,061 |
| `currentYear_liabilities_total` | `BAL_liabilities_total_curr` | 285,508 |
| `avg_equity` | `AVERAGE(startYear_equity, currentYear_equity)` | 65,341.5 |
| `avg_total_assets` | `AVERAGE(startYear_total_assets, currentYear_assets_total)` | 362,110.5 |
| `avg_total_capitalization` | `AVERAGE(startYear_total_capitalization, currentYear_total_capitalization)` | 147,380.5 |

### 5. Ratio Definitions & Formulas

All formulas in named-range notation. Expected FY2025 values shown for validation.

**Performance**

| Ratio | Formula | Unit | Value |
|-------|---------|------|------:|
| MVA | `market_capitalization − currentYear_equity` | $M | 3,700,244 |
| Market-to-Book | `market_capitalization / currentYear_equity` | x | 51.18 |
| EVA | `currentYear_after_tax_operating_income − (cost_capital × startYear_total_capitalization)` | $M | 99,880.5 |

**Profitability**

| Ratio | Formula | Unit | Value |
|-------|---------|------|------:|
| ROA | `currentYear_after_tax_operating_income / startYear_total_assets` | % | 30.69% |
| ROC | `currentYear_after_tax_operating_income / startYear_total_capitalization` | % | 78.49% |
| ROE | `INC_net / startYear_equity` | % | 196.68% |
| ROA [avg] | `currentYear_after_tax_operating_income / avg_total_assets` | % | 30.93% |
| ROC [avg] | `currentYear_after_tax_operating_income / avg_total_capitalization` | % | 76.00% |
| ROE [avg] | `INC_net / avg_equity` | % | 171.42% |

**Efficiency**

| Ratio | Formula | Unit | Value |
|-------|---------|------|------:|
| Asset Turnover `RATIO_asset_turnover` | `INC_sales / startYear_total_assets` | x | 1.140 |
| Receivables Turnover | `INC_sales / startYear_receivables` | x | 6.282 |
| Avg Collection Period | `startYear_receivables / currentYear_daily_sales_average` | days | 58.10 |
| Inventory Turnover | `INC_cost_goods_sold / startYear_inventory` | x | 30.33 |
| Days in Inventory | `startYear_inventory / currentYear_cost_goods_sold_daily` | days | 12.04 |
| Profit Margin | `INC_net / INC_sales` | % | 26.92% |
| Operating Profit Margin `RATIO_operating_profit_margin` | `currentYear_after_tax_operating_income / INC_sales` | % | 26.92% |

**Leverage**

| Ratio | Formula | Unit | Value |
|-------|---------|------|------:|
| Long-term Debt Ratio | `currentYear_debt_long_term / (currentYear_debt_long_term + currentYear_equity)` | % | 51.51% |
| Long-term Debt-Equity | `currentYear_debt_long_term / currentYear_equity` | x | 1.062 |
| Total Debt Ratio | `currentYear_liabilities_total / currentYear_assets_total` | % | 79.48% |
| Times Interest Earned | `INC_ebit / INC_interest_expense` | x | n/a (no interest exp.) |
| Cash Coverage | `(INC_ebit + INC_depreciation) / INC_interest_expense` | x | n/a (no interest exp.) |
| Debt Burden `RATIO_debt_burden` | `INC_net / currentYear_after_tax_operating_income` | x | 1.000 |
| Leverage Ratio `RATIO_leverage` | `currentYear_assets_total / currentYear_equity` | x | 4.872 |

**Liquidity**

| Ratio | Formula | Unit | Value |
|-------|---------|------|------:|
| Net Working Capital to Assets | `currentYear_working_capital_net / currentYear_assets_total` | % | −4.92% |
| Current Ratio | `currentYear_assets_current / currentYear_liabilities_current` | x | 0.893 |
| Quick Ratio | `(currentYear_cash_marketable_securities + BAL_receivables_curr) / currentYear_liabilities_current` | x | 0.771 |
| Cash Ratio | `currentYear_cash_marketable_securities / currentYear_liabilities_current` | x | 0.330 |

**Du Pont**

| Ratio | Formula | Unit | Value |
|-------|---------|------|------:|
| ROA Decomposition | `RATIO_asset_turnover × RATIO_operating_profit_margin` | % | 30.69% |
| ROE Decomposition | `RATIO_leverage × RATIO_asset_turnover × RATIO_operating_profit_margin × RATIO_debt_burden` | % | 149.52% |

Use the `IFERROR(..., "n/a (no interest exp.)")` guard on Times Interest Earned and Cash Coverage because `INC_interest_expense = 0` for Apple.

### 6. Validation Rules

The executor must verify each before reporting results:

1. **Balance Sheet balances, both years:** `BAL_assets_total_curr = BAL_liabilities_total_curr + BAL_equity_shareholders_curr` (359,241) and the prior-year equivalent (364,980).
2. **Du Pont ROA identity:** `RATIO_asset_turnover × RATIO_operating_profit_margin` must equal direct ROA (30.69%) to 6 decimals. The inline check on `Ratios!F75` must display "✓ matches direct ROA".
3. **Du Pont ROE time-mismatch (expected, not an error):** Du Pont ROE (149.52%) will **not** equal direct ROE (196.68%) because the leverage component uses current-year balances while asset turnover uses prior-year (start-of-year) assets. This divergence must be explained in the analysis memo, not "fixed."
4. **No `#REF!` / `#DIV/0!`:** every ratio resolves to a number or the documented "n/a" string. A `#DIV/0!` signals an empty denominator named range.
5. **Prior-year cells populated:** all `startYear_*` ranges must have values, or start-of-year ratios (ROA, ROC, ROE, asset/inventory/receivables turnover) fail silently.
6. **Sign sanity:** retained earnings is legitimately negative (accumulated deficit + AOCI reclass); net working capital is legitimately negative (−17,674). No other line should be negative.
7. **Reclass disclosure:** the Notes tab must record the US-GAAP reclassifications (PP&E net only; no goodwill/intangibles; current marketable securities folded into cash; AR + vendor non-trade receivables combined; deferred revenue into other current liabilities; commercial paper + current term debt into short-term debt; accumulated deficit + AOCI into retained earnings).

---

## Part B — Analysis Specification

### 7. Analysis Requirements

For each category, interpret the level, the trend vs. FY2024 where derivable, and cross-category linkages. Benchmarks: Apple's own prior year, large-cap US tech peers (Microsoft, Alphabet), and general norms (current ratio ~1.5–2.0; total debt ratio < 60% as a conventional comfort line).

- **Performance:** Explain the extraordinary market-to-book (51x) and MVA ($3.7T) as the market capitalizing Apple's intangible/brand and capital-return engine that the GAAP balance sheet does not record. Tie EVA ($99.9B positive) to value creation well above the 8.5% cost of capital.
- **Profitability:** ROE (196.68%) and ROC (78.49%) are inflated by a thin, buyback-depleted equity base, not purely operating excellence — connect to leverage. Contrast with the more stable averaged variants.
- **Efficiency:** Strong inventory turnover (30.3x; 12 days) reflects Apple's supply-chain model. Asset turnover (1.14x) and 58-day collection period give the operating-efficiency picture feeding Du Pont.
- **Leverage:** Total debt ratio 79.48% and leverage ratio 4.87x are driven by negative retained earnings (buybacks), not distress — frame as a deliberate capital-return strategy, supported by zero net interest expense.
- **Liquidity:** Current 0.89, quick 0.77, cash 0.33, negative net working capital. Argue why this is sustainable for Apple (supplier financing, predictable cash generation, $54.7B cash) rather than a red flag.

### 8. Du Pont Decomposition

Decompose ROE = `leverage × asset_turnover × operating_profit_margin × debt_burden`. Identify the **primary driver**: state which of the four components contributes most to Apple's ROE and quantify each. Assess sustainability — distinguish margin/efficiency-driven return (durable) from leverage-driven return (a function of the shrinking equity base from buybacks). Explicitly explain the Du Pont-ROE vs. direct-ROE gap (Rule 6.3) as a deliberate prior-year vs. current-year balance timing mismatch in the model, and state which figure better represents economic return.

### 9. Strategic Recommendations

Provide **3–5** recommendations. Each must: (a) cite specific ratio evidence by name and value; (b) state the financial implication; (c) be actionable and specific (a decision a CFO/board could act on), not generic ("improve efficiency"). At least one must address the capital-structure / negative-equity question and at least one the sub-1.0 liquidity position. Flag any recommendation whose support depends on the known model limitations in Section 6.

### 10. Output Format

- **Format:** Markdown memo, ~1,200–1,800 words (3–5 pages).
- **Audience / tone:** Finance-literate reviewer; analytical and direct; define a metric only when its interpretation is non-obvious for Apple.
- **Structure (in order):**
  1. **Executive Summary** — 4–6 sentences: overall financial health verdict.
  2. **Company & Data Basis** — period, standard, currency, source filing, key reclassifications.
  3. **Ratio Analysis by Category** — Performance, Profitability, Efficiency, Leverage, Liquidity; each with a results table (ratio · value · brief read).
  4. **Du Pont Decomposition** — component table + driver/sustainability narrative + the ROE-gap explanation.
  5. **Strategic Recommendations** — numbered 3–5, each in the (a)/(b)/(c) form from Section 9.
  6. **Limitations & Validation** — results of the Section 6 checks and the model's prior-year/current-year timing caveat.
- **Ratio presentation:** percentages to 2 decimals, multiples ("x") to 2 decimals, currency in $M (or $T where clearer for market cap/MVA).

---

## References

1. Apple Inc. Form 10-K, FY2025 (ended Sep 27, 2025), filed Oct 31, 2025 — SEC EDGAR, CIK 0000320193: https://www.sec.gov/cgi-bin/browse-edgar?action=getcompany&CIK=0000320193&type=10-K
2. Source model: `models/builds/2026-05-16-pham-apple-financials.xlsx` (Stage 3 populated workbook).
3. Instructor template: `models/templates/performance-ratios-template.xlsx`.
4. Spec template: `docs/templates/spec-template.md` (raw: https://raw.githubusercontent.com/adamwstauffer/shidler/main/docs/templates/spec-template.md).
5. Stage 4 brief: `courses/BUS-629-VEMBA-International-Corporate-Finance/stage4-technical-specification.md`.
6. Auditor: Ernst & Young LLP — unqualified opinion on FY2025 financial statements.
