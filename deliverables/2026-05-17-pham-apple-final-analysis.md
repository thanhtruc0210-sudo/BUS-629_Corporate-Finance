---
template: final-analysis
purpose: "Stage 5 evaluated final analysis — corrected, annotated, and edited version of the cold-LLM output, with corrections and LLM evaluation"
author: Truc Pham
date: 2026-05-17
company: Apple Inc. (AAPL)
fiscal_period: FY2025 (year ended Sep 27, 2025) vs FY2024
stage: 5
parent_llm_output: deliverables/2026-05-17-pham-apple-llm-raw.md
parent_verification: analysis/validation/2026-05-17-pham-apple-stage5-verification.md
parent_spec: docs/specs/2026-05-17-pham-apple-spec.md
status: FINAL — evaluated final analysis for BUS-629 project
---

# Apple Inc. (AAPL) — FY2025 Performance Ratio Analysis (Final)

**Author:** Truc Pham
**Date:** 2026-05-17
**Project:** BUS-629 Stage 5 — Evaluated final analysis

---

## Executive Summary

Apple Inc. closed FY2025 as an operationally elite firm executing a deliberate capital-return strategy that distorts headline equity ratios well beyond their economic meaning. The firm produced $112.0B of net income on $416.2B of revenue and a $359.2B asset base, yielding **ROA of 30.69%, ROC of 78.49%, and direct ROE of 196.68%**. Market capitalization of $3.77 trillion implies a **market-to-book multiple of 51.18×** and an **MVA of $3.70 trillion**, while **EVA of $99.9B** confirms genuine value creation against an 8.5% cost of capital.

The headline ROE is not a profitability signal — it is a capital-structure signal. Apple has shrunk book equity through $90.7B of FY2025 buybacks, leaving the equity base ($73.7B) at roughly 20% of total assets. **The analytical conclusion: anchor profitability assessment on ROA and ROC, treat ROE as a derived structural metric, and recognize that classical liquidity thresholds (current ratio < 1.0) require re-framing for a firm of Apple's cash-flow profile.**

---

## 1. Company & Data Summary

This analysis covers **Apple Inc. (NASDAQ: AAPL)**, SEC CIK 0000320193, for **FY2025** (52-week year ended September 27, 2025) with FY2024 (year ended September 28, 2024) as the start-of-year comparative. Figures drawn from Form 10-K filed October 31, 2025, audited by Ernst & Young LLP under US GAAP, unqualified opinion. Reporting currency is USD; values in millions.

**Seven US-GAAP reclassifications** were applied to fit the model architecture:

1. PP&E reported net only ($49,834M)
2. Goodwill and intangibles set to zero (Apple reports neither separately)
3. Current marketable securities folded into cash ($54,697M)
4. Accounts receivable includes vendor non-trade receivables
5. Deferred revenue consolidated into other current liabilities
6. Commercial paper plus current term debt consolidated into short-term debt ($20,329M)
7. Accumulated deficit plus AOCI rolled into retained earnings (−$19,835M)

**Market & disclosed data (from NASDAQ and 10-K):**
- Share price: $255.46 (FY2025 fiscal year-end close, Sep 26, 2025) — *NASDAQ disclosed*
- Shares outstanding: 14,773.26M (diluted weighted-average, FY2025) — *Apple 10-K disclosed*
- Effective tax rate: 15.6% (computed: $20,719M provision ÷ $132,729M pretax income) — *derived from 10-K*

**Analyst assumption (derived, not disclosed):**
- Cost of capital: 8.5% (CAPM-derived: 4.0% risk-free + 1.10 beta × 5.0% equity risk premium, with after-tax debt adjustment for Apple's capital structure)

**Data quality note:** Each ratio was cross-checked against the Stage 3 workbook and five representative ratios were manually re-computed (see `analysis/validation/2026-05-17-pham-apple-stage5-verification.md`). All five reconciled exactly to LLM-stated values. No arithmetic errors detected.

---

## 2. Ratio Results & Interpretation

### 2.1 Performance Ratios

| Metric | Value |
|---|---|
| Market Capitalization | $3,773,977M |
| MVA | $3,700,244M |
| Market-to-Book | 51.18× |
| EVA | $99,880.5M |

The **51.18× market-to-book multiple** indicates equity holders pay $51 for every dollar of recorded book value. GAAP cannot justify this multiple on the asset side because it does not capitalize Apple's brand, installed base, Services ecosystem, or the buyback machinery that has shrunk equity faster than retained earnings can grow it.

**EVA of $99.9B** corroborates the market's view internally. After-tax operating income of $112.0B exceeds the capital charge of $12.1B (8.5% × $142.7B prior-year capitalization) by nearly $100B annually. Together, MVA, M/B, and EVA point to the same conclusion: **Apple earns far above its cost of capital, and book equity is the wrong scale on which to measure firm value.**

### 2.2 Profitability Ratios

| Metric | Value | Comment |
|---|---|---|
| ROA (start-of-year) | 30.69% | $112,010M ÷ $364,980M |
| ROA (average) | 30.93% | $112,010M ÷ $362,110M |
| ROC (start-of-year) | 78.49% | $112,010M ÷ $142,700M |
| ROC (average) | 76.00% | $112,010M ÷ $147,381M |
| ROE (direct) | **196.68%** | $112,010M ÷ $56,950M start equity |
| ROE (average) | 171.42% | $112,010M ÷ $65,342M avg equity |

**ROA of 30.69%** is industry-leading. The averaged variant (30.93%) confirms the asset base is genuinely productive — not artificially shrunk. **ROC of 78.49%** shows the long-term capital structure earns nearly 80 cents per dollar invested. These ratios are not sustainable under perfect competition; they reflect deep economic moats.

**ROE of 196.68% requires careful interpretation.** Apple is not "twice as profitable per dollar of book equity" in real economic terms — the figure is inflated because management spent $90.7B in FY2025 alone repurchasing shares, driving the equity base toward zero. **ROC and ROA are the cleaner profitability signals; ROE is a hybrid metric blending operating excellence with capital-return policy.** The Du Pont decomposition (§2.6) quantifies the split between "real" operating return and leverage geometry.

### 2.3 Efficiency Ratios

| Metric | Value | Comment |
|---|---|---|
| Asset Turnover | 1.140× | $416,161M ÷ $364,980M |
| Inventory Turnover | 30.33× | $220,960M ÷ $7,286M (start-of-year) |
| Days in Inventory | 12.04 days | Just-in-time supply chain |
| Receivables Turnover | 6.282× | $416,161M ÷ $66,243M |
| Days Sales Outstanding | 58.10 days | Manually verified |
| Net Profit Margin | 26.92% | $112,010M ÷ $416,161M |
| Operating Profit Margin | 26.92% | Identical to net margin (zero interest expense) |

Efficiency metrics show a tight operation. **Inventory turnover of 30.33×** translates to just 12 days of inventory on hand — evidence of just-in-time supply-chain discipline. Inventory shrank further in FY2025 from $7,286M to $5,718M ($1,400M source of cash). This could indicate tightening operational discipline OR a deliberate run-down ahead of a product transition — FY2026 results will distinguish.

**DSO of 58.10 days** is longer than a pure consumer retailer would tolerate but normal for a business mixing enterprise, channel-partner, and carrier receivables with direct retail. Receivables grew during the year ($66.2B → $73.0B, $7.0B use of cash), implying collection may be lengthening at the margin — a watch item.

**Operating and net margin are identical (26.92%)** because Apple's net interest expense is zero — investment income on the $90B+ marketable-securities portfolio offsets interest on $98B+ gross debt. This is itself an analytical signal: a firm of Apple's debt scale generating zero net interest cost operates treasury as a profit center.

### 2.4 Leverage Ratios

| Metric | Value | Comment |
|---|---|---|
| Total Debt Ratio | 79.48% | $285,508M ÷ $359,241M |
| LT Debt Ratio | 51.51% | $78,328M ÷ $152,061M |
| LT Debt-Equity | 1.062× | $78,328M ÷ $73,733M |
| Times Interest Earned | n/a | Net interest expense = $0 |
| Cash Coverage | n/a | Net interest expense = $0 |
| Debt Burden | 1.000 | NI = NOPAT (no wedge) |
| **Leverage Multiplier** | **4.872×** | Assets / Equity — drives Du Pont ROE |

Apple's leverage profile **looks aggressive but tells a different story when decomposed.** Total debt ratio of 79.48% sits well above the 60% conventional comfort line, and the leverage multiplier of 4.87× drives the inflated ROE. But Apple is not "leveraged" in the distressed sense — it is *un-equity-zed*. **The denominator has been shrunk on purpose:** cumulative buybacks have returned more capital than retained earnings have replaced.

**TIE and Cash Coverage report "n/a"** because net interest expense is zero — itself a leverage signal. A firm with $98.7B in gross debt and zero net interest cost generates enough investment income to fully offset borrowing — a treasury capability most peers lack. The degenerate solvency ratios should be read as evidence of financial strength, not as missing data.

**Debt burden of 1.000** confirms no interest or tax wedge at the marginal level — every dollar earned operationally arrives at the bottom line. The seven leverage metrics together describe a **deliberately capital-light equity structure**, not balance-sheet stress.

### 2.5 Liquidity Ratios — Re-framing Required

| Metric | Value | Classical Reading | Re-framed Reading |
|---|---|---|---|
| Current Ratio | 0.893 | "Concerning" — below 1.5–2.0 norm | **Efficient** — supplier financing |
| Quick Ratio | 0.771 | Weak | Adequate given $111.5B OCF |
| Cash Ratio | 0.330 | Below conservative norms | Deliberate optimization |
| NWC / Assets | −4.92% | Negative | A feature, not a defect |

**For most firms, a current ratio of 0.893 would be a warning. For Apple, it is the by-product of efficient working-capital management.** Three structural facts support the re-framing:

1. **Negotiated supplier financing.** $69,860M of accounts payable functions as interest-free funding from a concentrated supply base, with longer duration than Apple's own 58-day collection cycle.

2. **Operating cash machine.** FY2025 operating cash generation was $111.5B — Apple produces in roughly two months what it would take to cover the entire $17.7B current-liability gap.

3. **Cash position is a policy variable, not a constraint.** The $54.7B in cash and marketable securities is a deliberate downward optimization from $65.2B in FY2024 (management redirected $10.5B to the buyback program). The buyback dial controls the cushion.

Negative net working capital is, for Apple, a feature — not a defect — of the cash-conversion model.

### 2.6 Du Pont Decomposition — The Interpretive Centerpiece

The Du Pont system separates operating performance from capital-structure effects. This is the most important section of the analysis.

#### ROA Decomposition (simple)

**ROA = Asset Turnover × Operating Profit Margin = 1.140 × 26.92% = 30.69%**

Direct ROA reconciles exactly. Margin is the larger driver — Apple's ROA is structurally a **margin story**, not a turnover story. The hardware-plus-services model has tight ceilings on turnover; further ROA expansion must come from margin (Services mix, manufacturing efficiency, ASP-positive product transitions).

#### ROE Decomposition (the four-lever identity)

**ROE = Leverage × Asset Turnover × Operating Margin × Debt Burden**
**= 4.872 × 1.140 × 26.92% × 1.000 = 149.52%**

| Component | Value | Type | Sustainability |
|---|---|---|---|
| Leverage | 4.872× | Capital-return policy | Policy variable |
| Asset Turnover | 1.140× | Operating productivity | Durable (model ceiling) |
| Operating Margin | 26.92% | Pricing + mix + cost discipline | Durable, mix-led upside |
| Debt Burden | 1.000 | Tax + financing efficiency | Stable while net interest = 0 |

**Primary level driver: Leverage (4.872×).** Operating ROA of 30.69% is multiplied to 149.5% almost entirely through the assets-to-equity ratio. Apple's ROE rests on margin × turnover (the ROA core); financially, it is multiplied by leverage that reflects shareholder-return policy, not borrowing aggression.

**The Direct-vs-Du Pont ROE gap (47 percentage points).** Direct ROE (196.68%) exceeds Du Pont ROE (149.52%) by 47 percentage points. This is **not a calculation error**:

- **Direct ROE** uses start-of-year equity ($56,950M, before FY2025 retained earnings replenished it). It answers: *"What return did shareholders earn on the equity they started the year with?"* — period attribution.
- **Du Pont ROE** uses current-year equity ($73,733M, larger after the year's retained earnings addition). It answers: *"What is the steady-state return implied by today's capital structure?"* — sustainability.

Both are correct under their own definitions. For steady-state economic interpretation, Du Pont ROE (149.52%) is the appropriate measure; Direct ROE (196.68%) is the period-historical measure.

**Sustainability commentary.** Margin (26.92%) and turnover (1.14×) are operationally durable. Leverage (4.87×), being a function of the buyback dial, is a policy variable. **If Apple paused buybacks tomorrow, equity would grow with retained earnings and ROE would compress toward roughly 2× ROA, or ~60%.** The 196.68% ROE is therefore *real but not steady-state.*

---

## 3. LLM Evaluation & Annotations

This section evaluates the cold LLM's execution of the Stage 4 spec — the central learning artifact of Stage 5.

### 3.1 What the LLM Executed Correctly

The cold LLM (Claude Opus 4.7, fresh session, spec-only input) executed the spec with exceptional fidelity:

✅ **Mathematical accuracy: 5 of 5 verified ratios match exactly.** No hallucinated values, no arithmetic errors. (See `analysis/validation/2026-05-17-pham-apple-stage5-verification.md`.)

✅ **Convention discipline.** The LLM honored every spec convention — 365-day year (not banker's 360), start-of-year denominators where specified, named-range definitions, and the year-suffix mapping (`_2020` = FY2025, `_2019` = FY2024) that was the focus of the Stage 4 HIL iteration.

✅ **Anomaly framing.** Sub-1.0 current ratio was correctly re-framed as efficient working-capital management with three supporting structural facts — not flagged as a liquidity risk.

✅ **Du Pont reconciliation.** The 47-point Direct-vs-Du Pont ROE gap was correctly explained as a structural time-mismatch (Validation Check 6.3), not as an arithmetic error. The LLM did not panic-flag.

✅ **Output structure.** Section 11's format requirements were followed exactly — all required sections present, word counts in target range, professional tone throughout.

### 3.2 Where the LLM Deviated, Hallucinated, or Oversimplified

⚠️ **Misclassified disclosed data as "analyst assumptions."** The LLM's "Company & Data Summary" section grouped share price ($255.46) and shares outstanding (14,773.26M) under "Analyst assumptions" alongside cost of capital. This is incorrect — share price is NASDAQ-disclosed real market data, and shares outstanding is disclosed in the 10-K. Only **cost of capital (8.5%)** is a genuine analyst-derived assumption (CAPM-built). This corrected classification is reflected in §1 of this final analysis. **Spec gap:** §3.3 of the Stage 4 spec listed all three under the same heading without distinguishing disclosed-vs-derived, which led to the conflation.

⚠️ **Asset divestitures interpretation.** The LLM stated: *"the asset base is genuinely productive, not artificially shrunk through one-off divestitures."* This is a defensible interpretation of stable ROA across denominators, but it overstates what the ratio alone proves. Confirming or denying material divestitures requires 10-K investing-activities and segment disclosures — which the LLM did not have. This is a **spec-induced limitation**, not a hallucination.

⚠️ **Receivables interpretation drift.** The LLM noted receivables grew "implying collection may be lengthening at the margin." Fair inference, but the more disciplined move is to compute DSO at both year-ends and report the trend explicitly. The spec did not require this.

⚠️ **Strategic observations with weak trade-off discussion.** The LLM's recommendations named absolute targets without addressing how those targets would interact with credit-rating implications or peer norms.

⚠️ **No peer benchmarking.** Targets are named in absolute terms without anchoring to peer levels (MSFT, GOOGL, META). The spec did not require this and the LLM had no peer data — a **spec gap** rather than an LLM failure.

### 3.3 Errors Caused by Spec Gaps vs. LLM Limitations

**Spec gaps (responsibility of the spec author):**

1. **§3.3 conflated disclosed data and analyst assumptions** under a single "analyst assumption" heading. The LLM faithfully repeated this conflation. The fix: separate disclosed market data (share price, shares outstanding) from derived analyst inputs (cost of capital) explicitly in the spec.

2. **§8.4 did not specify how to interpret degenerate solvency ratios** (TIE = n/a when interest = 0). The LLM handled it correctly only because it had analytical maturity; a less capable LLM would have flagged it as missing data.

3. **§8.6 did not specify which ROE to "headline"** in interpretation. The LLM reported both 196.68% and 149.52% side-by-side without ranking. *This is the single most consequential spec gap.*

4. **§10 did not require recommendations to benchmark against named peers** — leading to absolute targets without comparable anchoring.

**LLM limitations (intrinsic to spec-only execution):**

1. No access to peer-set data — couldn't benchmark MVA, M/B, or operating margin against MSFT/GOOGL/META.

2. No access to 10-K narrative — couldn't confirm or refute interpretations of divestiture history or strategic context.

3. No real-time market data — couldn't adjust for share-price moves between FY-end and analysis date.

---

## 4. Strategic Observations

Five observations derived from the ratio analysis. Each cites specific ratio evidence and names the analytical implication.

### O1 — ROE Communication and Book-Equity Geometry

**Evidence:** ROE of 196.68% materially exceeds ROC (78.49%) and ROA (30.69%); the Direct-vs-Du Pont ROE gap is 47 percentage points; the leverage multiplier of 4.872× sits on equity of $73.7B that has been compressed by $90.7B of FY2025 buybacks.

**Implication:** The ROE headline number carries information about capital structure decisions, not operating performance. Profitability comparisons across firms or across years are more defensibly anchored on ROC and ROA. When ROE is reported, Du Pont ROE (149.52%) is the steady-state measure; Direct ROE (196.68%) is the period-historical measure. The two should be communicated together, not separately.

### O2 — Liquidity Re-framing

**Evidence:** Current ratio 0.893, quick 0.771, cash 0.330, NWC −$17.7B — all below conservative norms. Operating cash flow of $111.5B and cash + marketable securities of $54.7B make the sub-1.0 reading sustainable on cash-flow grounds.

**Implication:** Classical liquidity thresholds (current ratio ≥ 1.5) do not apply to firms with Apple's cash-flow profile. A more appropriate framework is operating cash flow as a multiple of current liabilities (here: $111.5B / $165.6B = 0.67× annually, meaning Apple generates two-thirds of its current-liability balance in cash every year). Absent a documented liquidity policy, however, the firm has no governance trip-wire against future deterioration.

### O3 — Book Equity as a Residual

**Evidence:** FY2025 buybacks of $90.7B drove retained earnings to −$19.8B; total financing outflow ($114.6B = buybacks + dividends + net debt actions) exceeded operating cash flow of $111.5B; the $3.1B gap was closed by net investing inflows of $15.2B (asset sales offsetting capex).

**Implication:** Book equity has become a residual of the buyback program, not an independent capitalization decision. The leverage multiplier (4.87×) and the ROE inflation that follows are mechanical consequences of this residual treatment. A book-equity floor would provide governance discipline; absent one, the equity base will continue to compress at the marginal cost of the buyback dial.

### O4 — Free Cash Flow Disclosure Clarity

**Evidence:** FCF using the conventional definition = $111.5B operating cash flow − $12.7B capex = **$98.8B**. This differs materially from any reading that nets the $29.4B in asset sales against capex (which would inflate "FCF" to ~$128B). The +$15.2B net-investing line in the cash flow statement reflects securities-portfolio rebalancing, not strategic asset disposition.

**Implication:** Analyst communication should distinguish operating FCF ($98.8B) from securities-portfolio activity. The two should not be netted. This affects how the firm's cash-generation profile is compared with peers and how DCF-based valuations are constructed.

### O5 — Margin × Turnover as the Operating Signal

**Evidence:** Operating profit margin 26.92% × asset turnover 1.140× = ROA 30.69% (Du Pont ROA reconciliation confirmed).

**Implication:** This product is the genuine operating return — immune to capital-return policy decisions. For performance measurement, the margin × turnover decomposition is more informative than ROE. This observation rests on the FY2025 zero-interest-expense assumption holding; if FY2026 net interest cost re-emerges, debt burden will diverge from 1.000 and the relationship between operating ROA and ROE will need re-examination.

---

## 5. Validation Notes

Per Stage 4 spec Section 7 (Validation Rules):

| # | Check | Result |
|---|---|---|
| 1 | Balance sheet balances FY2025 | ✓ $359,241M assets = $285,508M liabilities + $73,733M equity |
| 2 | Balance sheet balances FY2024 | ✓ $364,980M = $308,030M + $56,950M |
| 3 | Du Pont ROA identity | ✓ 1.140 × 26.92% = 30.69%, matching direct ROA |
| 4 | Du Pont ROE timing-mismatch | Expected: Du Pont (149.52%) ≠ Direct (196.68%); 47-pt gap is structural time-mismatch, not error |
| 5 | No `#REF!` / `#DIV/0!` | ✓ All formulas resolve; TIE and Cash Coverage report "n/a" via IFERROR guard |
| 6 | Prior-year cells populated | ✓ All `startYear_*` ranges have values |
| 7 | Sign sanity | ✓ Retained earnings legitimately negative (−$19,835M); NWC legitimately negative; no other impossible negatives |
| 8 | Reclass disclosure | ✓ All seven US-GAAP reclassifications documented (see §1) |

**Manual ratio verification:** 5 of 5 ratios match exactly between manual computation and LLM-stated values. See `analysis/validation/2026-05-17-pham-apple-stage5-verification.md`.

---

## 6. Executive Justification

Most ratio analyses begin with a single question — Is this firm worth lending to? Worth investing in? Worth restructuring? — and end with a recommendation. Apple's FY2025 ratios reward a different discipline. The ratios here are not the answer; they are the inputs to a framing decision about which numbers to trust as economic signals and which to treat as derivatives of capital-allocation policy.

In technology-sector finance, the boundary between operational performance and capital-return policy has blurred progressively over the past several years. Software-and-services firms generate cash structurally faster than they can re-deploy it operationally. When the cash conversion is sustained — as Apple's $111.5B annual operating cash flow demonstrates — book equity becomes a managed variable, not a fixed parameter. The buyback is no longer an annual decision; it is a continuous-operations function of the treasury, governed by share-price triggers, cash thresholds, and authorization limits. Equity ratios, in this regime, lose their independence from policy.

The practical implication for ratio analysis is straightforward. ROA and ROC remain trustworthy because their denominators (total assets, total capitalization) are operationally determined — assets exist because operations require them, capitalization exists because the cost of capital is paid on it. ROE loses that property when book equity is a residual. The 196.68% ROE Apple reported in FY2025 is not "twice as profitable as last year" — it is the same operating engine multiplied by a buyback dial that turned more aggressively. Reporting it without that context misleads.

This perspective shapes every framing choice in this analysis. Leading with Du Pont ROE rather than Direct ROE, re-framing the current ratio rather than flagging it, anchoring profitability on ROA and ROC rather than ROE, separating disclosed market data from derived analyst assumptions — these are deliberate decisions, not arithmetic outputs. They are the choices a head-of-finance role demands daily: deciding which metrics carry information and which carry policy, distinguishing observed data from derived estimates, and ensuring the analytical communication reflects those distinctions.

The cold LLM's arithmetic was flawless; its framing instincts were generic, and its data classification (lumping share price and shares outstanding with cost of capital as "analyst assumptions") reflects exactly the kind of categorical sloppiness that experienced finance practitioners learn to avoid. The analytical contribution of this final analysis is the framing — recognizing where classical interpretive rules break down at the boundary between balance-sheet metrics and policy outputs, correcting data classifications, and articulating the measurement architecture that aligns reported numbers with the decisions that drive them. That is the work that a spec, however precise, cannot fully encode; it is the work the human reviewer brings.

---

## References

1. Apple Inc. Form 10-K, fiscal year ended September 27, 2025. Filed October 31, 2025. SEC EDGAR Accession 0000320193-25-XXXXXX. Auditor: Ernst & Young LLP, unqualified opinion.

2. Stage 4 technical specification, `docs/specs/2026-05-17-pham-apple-spec.md`, v1.1, Truc Pham, 2026-05-17.

3. Stage 3 populated workbook, `models/builds/2026-05-16-pham-apple-financials.xlsx`.

4. Stage 5 raw LLM output, `deliverables/2026-05-17-pham-apple-llm-raw.md` (Claude Opus 4.7, cold execution, 2026-05-17).

5. Stage 5 manual verification table, `analysis/validation/2026-05-17-pham-apple-stage5-verification.md`.

6. Stage 5 spec retrospective, `deliverables/2026-05-17-pham-apple-spec-retrospective.md` *(forthcoming)*.

7. NASDAQ market data, AAPL closing price September 26, 2025.

---

*Final analysis authored by Truc Pham, 2026-05-17. Word count: ~3,750 words.*
