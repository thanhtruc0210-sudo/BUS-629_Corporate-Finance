---
template: stage5-verification
purpose: "Manual recomputation of ≥5 ratios from Stage 3 financials to cross-check LLM-generated analysis"
author: Truc Pham
date: 2026-05-17
company: Apple Inc. (AAPL)
fiscal_period: FY2025 (year ended Sep 27, 2025) vs FY2024
stage: 5
parent_llm_output: 2026-05-17-pham-apple-llm-raw.md
parent_spec: 2026-05-17-pham-apple-spec.md
parent_workbook: 2026-05-16-pham-apple-financials.xlsx
---

# Stage 5 Manual Ratio Verification — Apple Inc. FY2025

**Author:** Truc Pham
**Date:** 2026-05-17
**Compared against:** LLM raw output (`deliverables/2026-05-17-pham-apple-llm-raw.md`)
**Source workbook:** `models/builds/2026-05-16-pham-apple-financials.xlsx`

---

## Purpose

This artifact recomputes ≥5 ratios **by hand** from Stage 3 financials and compares against the LLM's stated values. Per Stage 5 rubric (10% of stage grade), discrepancies are the most informative rows — each one tells me whether the LLM's analysis is trustworthy and where my Stage 4 spec might have gaps.

**Selection strategy.** I picked 5 ratios that span all six ratio categories AND exercise the conventions most likely to trip an LLM: averaging convention, start-of-year denominators, day-count conventions, multi-component decomposition, and definitional variants.

---

## Three Value Sources

Per Stage 5 brief, I am explicit about which two sources I am comparing:

| Source | Where it comes from | Used in this table |
|---|---|---|
| **Template auto-computed** | Stage 3 workbook's Ratios tab | Sanity check (column 5) |
| **LLM's stated** | Stage 5 raw LLM output | "LLM's Value" column |
| **My manual** | Hand-computed below from Stage 3 financials | "Manual Value" column |

The graded comparison is **Manual vs. LLM**. The template auto-computed values are a triangulation reference.

---

## Verification Table

| # | Ratio | Formula (named-range notation) | Manual Value (arithmetic shown) | LLM's Value | Match? | One-line note |
|---|---|---|---|---|---|---|
| 1 | **ROA (start-of-year)** | `currentYear_after_tax_operating_income / startYear_total_assets` | $112,010M / $364,980M = **30.69%** | 30.69% | ✓ | LLM used start-of-year denominator, consistent with spec §6.2 |
| 2 | **Days Sales Outstanding (DSO)** | `startYear_receivables / (INC_sales / 365)` | $66,243M / ($416,161M / 365) = $66,243M / $1,140.17M = **58.10 days** | 58.10 days | ✓ | LLM used 365-day convention correctly; SOY receivables correctly identified |
| 3 | **Inventory Turnover** | `INC_cost_goods_sold / startYear_inventory` | $220,960M / $7,286M = **30.33×** | 30.33× | ✓ | LLM correctly used FY2024 SOY inventory, not FY2025 current |
| 4 | **Du Pont ROE** | `RATIO_leverage × RATIO_asset_turnover × RATIO_operating_profit_margin × RATIO_debt_burden` | 4.8722 × 1.1402 × 26.92% × 1.0000 = **149.52%** | 149.52% | ✓ | Each component verified independently; LLM correctly flagged 47-pt gap vs. Direct ROE as time-mismatch (not error) |
| 5 | **Quick Ratio** | `(currentYear_cash_marketable_securities + BAL_receivables_2020) / currentYear_liabilities_current` | ($54,697M + $72,957M) / $165,631M = $127,654M / $165,631M = **0.771** | 0.771 | ✓ | LLM correctly included marketable securities in numerator (some implementations exclude) |

**Summary:** 5 / 5 match. No discrepancies in computed values.

---

## Detailed Computations

### Ratio 1: ROA (start-of-year)

**Spec formula (§6.2):** `currentYear_after_tax_operating_income / startYear_total_assets`

**Step-by-step:**
- After-tax operating income (NOPAT):
  - Net income FY2025: $112,010M
  - Interest expense (per LLM and spec): $0 (Apple FY2025 has zero net interest expense — investment income offsets borrowing cost)
  - Tax rate: 20,719 / 132,729 = 15.61%
  - NOPAT = $112,010 + (1 − 0.1561) × $0 = **$112,010M** (no tax shield because no interest)

- Start-of-year total assets: $364,980M (FY2024 balance sheet)

- **ROA = $112,010M / $364,980M = 30.69%**

**LLM's value:** 30.69% — **EXACT match.**

**Note:** The spec offers three ROA variants (start-of-year, current-year, average). The LLM consistently used start-of-year, which is the primary spec convention. The average-denominator alternative (using ($359,241 + $364,980)/2 = $362,110M) would yield 30.93% — a 24-basis-point spread that the LLM did not report. This is **acceptable** because the spec's §6.2 primary formula is start-of-year, but a strong analysis would note the alternative value for transparency.

### Ratio 2: Days Sales Outstanding

**Spec formula (§6.3):** `startYear_receivables / currentYear_daily_sales_average`

**Step-by-step:**
- Average daily sales = $416,161M / 365 days = **$1,140.17M/day**
- Start-of-year receivables: $66,243M (FY2024)
- **DSO = $66,243M / $1,140.17M = 58.10 days**

**LLM's value:** 58.10 days — **EXACT match.**

**Note:** The 365-day convention is correct per spec. A common LLM error is to use 360 days (banker's year), which would yield 57.31 days — a 0.8-day error. The LLM did NOT fall into this trap, demonstrating that the spec's explicit "365" specification was effective.

### Ratio 3: Inventory Turnover

**Spec formula (§6.3):** `INC_cost_goods_sold / startYear_inventory`

**Step-by-step:**
- COGS FY2025: $220,960M
- Start-of-year inventory (FY2024): $7,286M
- **Inventory Turnover = $220,960M / $7,286M = 30.33×**

**LLM's value:** 30.33× — **EXACT match.**

**Note:** This is the critical test of the year-suffix convention from spec §2.3 (the HIL iteration topic from Stage 4). A naïve LLM might use current-year inventory ($5,718M FY2025) which would yield 38.64× — a 27% error. The LLM correctly read the spec's intent: `_2019` in named ranges = Apple FY2024 = start-of-year. The Stage 4 HIL iteration paid off here.

**Bonus check — Days in Inventory:**
- Daily COGS = $220,960M / 365 = $605.37M/day
- Days in Inventory = $7,286M / $605.37M = **12.04 days**
- LLM stated: 12.04 days — **EXACT match.**

### Ratio 4: Du Pont ROE (4-component multiplication)

**Spec formula (§6.6):** `RATIO_leverage × RATIO_asset_turnover × RATIO_operating_profit_margin × RATIO_debt_burden`

**Component-by-component:**

| Component | Formula | Computation | Value |
|---|---|---|---|
| Leverage | `currentYear_assets_total / currentYear_equity` | $359,241M / $73,733M | **4.8722** |
| Asset Turnover | `INC_sales / startYear_total_assets` | $416,161M / $364,980M | **1.1402** |
| Operating Profit Margin | `currentYear_after_tax_operating_income / INC_sales` | $112,010M / $416,161M | **0.2692 (26.92%)** |
| Debt Burden | `INC_net / currentYear_after_tax_operating_income` | $112,010M / $112,010M | **1.0000** |

**Du Pont ROE = 4.8722 × 1.1402 × 0.2692 × 1.0000 = 1.4952 = 149.52%**

**LLM's value:** 149.52% — **EXACT match.**

**Critical observation — the 47-point gap vs. Direct ROE.** The Direct ROE (from §6.2) = $112,010M / $56,950M start-of-year equity = **196.68%**. The Du Pont ROE = **149.52%**. The gap is 47.16 percentage points. The LLM correctly identified this as a **time-mismatch** (Validation Check 6.3 in spec) — Direct ROE uses start-of-year equity ($56,950M), while Du Pont leverage uses current-year equity ($73,733M, larger because the year's retained earnings net of buybacks). Both are correct under their definitions. The LLM did NOT flag this as an error.

This is **high-quality analytical maturity** from the LLM — the spec's §6 validation rules allowed a ±2pp tolerance on Du Pont ROE reconciliation, but the actual gap is 47pp. A naïve executor would have flagged this as a failed validation. The LLM correctly understood that the gap is structural (timing convention), not arithmetic. **Credit to the spec for surfacing this distinction explicitly** in §7's analysis requirements.

### Ratio 5: Quick Ratio

**Spec formula (§6.5):** `(currentYear_cash_marketable_securities + BAL_receivables_2020) / currentYear_liabilities_current`

**Step-by-step:**
- Cash + marketable securities (current year): $54,697M
- Receivables (current year): $72,957M
- Current liabilities: $165,631M
- **Quick Ratio = ($54,697M + $72,957M) / $165,631M = $127,654M / $165,631M = 0.7707 ≈ 0.771**

**LLM's value:** 0.771 — **EXACT match.**

**Note:** A common quick-ratio variant excludes marketable securities (keeping only "cash equivalents"). The LLM included marketable securities, consistent with the template's `cash_marketable_securities` named-range definition. The spec was explicit about this; the LLM honored it.

---

## Summary of Findings

### Where the LLM excelled

✅ **Mathematical accuracy:** 5 of 5 verified ratios match exactly (to displayed precision). No arithmetic errors, no hallucinated values.

✅ **Convention discipline:** The LLM honored every convention specified — 365-day year, start-of-year denominators, named-range definitions, marketable-securities inclusion. The HIL iteration on year-suffix mapping (Stage 4) paid off here.

✅ **Analytical maturity:** The Du Pont vs. Direct ROE gap (47 percentage points) was correctly framed as a structural time-mismatch, not an error. The LLM did not panic-flag.

✅ **Anomaly framing:** Sub-1.0 current ratio (0.893) was correctly re-framed as efficient working-capital management with three supporting structural facts (supplier financing, operating cash generation of $111.5B, deliberate cash optimization). This was exactly the spec's §8.5 instruction.

### Discrepancies / observations worth noting

⚠️ **ROA reporting incomplete.** The LLM reported only start-of-year ROA (30.69%) without flagging that the average-denominator alternative (30.93%) exists in the spec §6.2. A senior analyst would have offered both. This is a **spec gap** — §6.2 lists three ROA variants but §8.2 only asks for one. **Forward-fix:** §8.2 should require reporting all three variants with the rationale for the primary.

⚠️ **Interest expense = $0 assumption underplayed.** The LLM treated zero interest expense as a clean fact, but Apple actually has $98.7B+ in gross debt; the $0 net interest reflects investment income offsetting interest cost — a classification choice, not an absence of interest. The LLM mentioned this once in the Leverage Ratios section but did not develop the implication: TIE and Cash Coverage are degenerate, which is itself a leverage signal. **Spec gap:** §8.4 should require explicit treatment of the "TIE = n/a" case rather than letting it fall through.

⚠️ **Du Pont ROE communication.** The LLM correctly explained the 47-point Direct-vs-Du Pont gap, but in real executive communication, reporting both 196.68% and 149.52% side-by-side without a recommended "headline" number is confusing. **Spec gap:** §8.6 should specify which to lead with for board communication and which to footnote.

### What this verification tells me about my Stage 4 spec

**Spec strengths confirmed:**
- The year-suffix convention warning (§2.3) was effective — no FY2024/FY2025 confusion.
- The 365-day specification (§5) was effective — no banker's-year error.
- The validation rules (§7) with tolerance bands prevented panic-flagging of the legitimate 47-point Du Pont ROE gap.

**Spec gaps surfaced** (for retrospective):
- §8.2 should require ALL three ROA variants reported, not one.
- §8.4 should require explicit handling of degenerate solvency ratios (TIE, Cash Coverage when interest expense is zero).
- §8.6 should specify the "lead" Du Pont measure for executive communication.

These three gaps are the foundation of the Stage 5 spec retrospective (deliverable #4).

---

## Conclusion

The LLM's mathematical execution of my Stage 4 spec was **flawless on the five verified ratios**. The most informative findings are **NOT discrepancies in numbers** (there are none) but **gaps in spec instructions** for how to *report and frame* ratios where multiple variants or degenerate cases exist. This is exactly the discipline Stage 5 is designed to teach: numerical correctness is necessary but not sufficient; analytical framing is where the spec earns its keep.

The Stage 4 HIL iteration on year conventions paid measurable dividends here. The Stage 5 retrospective will focus on framing and reporting completeness — the next layer of spec maturity.

---

*Verification compiled by Truc Pham, 2026-05-17. No AI used for the manual computations themselves; arithmetic shown step-by-step from Stage 3 workbook source values.*
