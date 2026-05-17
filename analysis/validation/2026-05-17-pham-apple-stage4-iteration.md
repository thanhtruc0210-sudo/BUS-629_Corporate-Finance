---
stage: 4
type: hil-iteration
method: option-3-annotated-diff
author: Truc Pham
date: 2026-05-17
spec_version_tested: 1.0
---

# Stage 4 HIL Iteration — Annotated Diff

## 1. Test Setup

- **LLM tested:** Claude Sonnet 4.6 (new conversation, zero prior context)
- **Prompt used:** "You are a financial analyst executor. Using ONLY the
  specification below, produce the deliverable it describes. Do not look up,
  infer, or estimate any figure not stated in the spec." — followed by the
  full text of `docs/specs/2026-05-17-pham-apple-spec.md` v1.0.
- **Spec version fed:** 1.0 (`2026-05-17-pham-apple-spec.md`)
- **Output reviewed:** `2026-05-17-pham-apple-ratio-analysis_1.md` (3,165 words)
- **Method note:** Option 3 (annotated diff). The v1.1 spec edits described in
  §3–§4 were applied to the spec file; §5 states the specific, checkable
  behavior changes those edits compel rather than a re-executed Round 2.

## 2. What the LLM Got Right

- **Both Balance-Sheet balance checks** confirmed exactly: FY2025
  $359,241 = $285,508 + $73,733 and FY2024 $364,980 = $308,030 + $56,950.
- **Du Pont ROA identity** verified: 1.140 × 26.92% = 30.69%, equal to direct ROA.
- **The hard case — Du Pont-ROE vs. direct-ROE gap.** It correctly explained the
  47.16 pp divergence (149.52% vs. 196.68%) as a deliberate prior-year vs.
  current-year denominator timing mismatch per Validation Rule 6.3, and stated
  which figure suits which audience. This was the spec's highest-risk
  instruction and it landed.
- **All ~30 ratios** reported with values matching the model to the stated precision.
- **Zero-interest handling:** correctly returned "n/a (no interest exp.)" for
  Times Interest Earned and Cash Coverage and explained debt burden = 1.000x.
- **Reclassification disclosure:** all seven US-GAAP reclasses reproduced accurately.
- **Recommendations** were actionable, specific, used the (a)/(b)/(c) structure,
  and covered the mandated capital-structure and sub-1.0 liquidity topics.
- **Derived sensitivities** (100 bps margin → ~5.5 pp Du Pont ROE; ~$4.2B EVA)
  were arithmetically correct and traceable to model inputs.

## 3. Issues Found & Fixes Applied

### Issue 1 — Cash Flow Statement materially incomplete (primary)
**What the LLM did:** The memo references only operating cash flow ($111.5B).
Financing activities (−$120,686M, incl. −$90,711M buybacks and −$15,421M
dividends) and the net increase in cash (+$5,991M) are entirely absent, as is
the working-capital bridge. There is no cash-flow section at all.
**Root cause in spec:** §3 v1.0 exposed only `CASH_operating` and
`CASH_investments` as the cash-flow data, and Part B (§7/§10) never required a
cash-flow narrative. An executor told to use *only* the spec literally had no
financing or net-cash-change data to report.
**Fix applied to spec:** §3 now lists the **complete** Cash Flow Statement —
operating bridge, investing breakdown, full **financing breakdown**, and **net
increase/(decrease) in cash** — with explicit values; §7 adds a required
**Cash-Flow Analysis** bullet and §10 adds it as deliverable section 4.

### Issue 2 — Free cash flow derived from the wrong line
**What the LLM did:** Recommendation 2 wrote "FY2025 free cash flow (operating
cash $111.5B less capex approximated by investing activities of $15.2B) exceeds
$96B." `CASH_investments` (+$15,195M) is a *net inflow* that nets +$29,390M of
asset sales against −$12,715M of capex; using it as a capex proxy is wrong, and
the ~$96B result was right only by coincidence (true FCF = 111,482 − 12,715 =
$98,767M).
**Root cause in spec:** §3 v1.0 did not expose the capital-expenditures line and
gave no warning that `CASH_investments` is a net figure, not capex.
**Fix applied to spec:** §3 now lists capex (−$12,715M) explicitly and adds a
boxed **caution**: FCF must be `CASH_operating − |capex|` = $98,767M, never
`CASH_operating − CASH_investments`.

### Issue 3 — Unsourced external claims used as evidence
**What the LLM did:** Asserted "Apple's Moody's Aaa / S&P AA+ ratings" and
"Microsoft and Alphabet operate similarly sub-standard current ratios" — neither
derivable from the spec, despite the spec's no-lookup rule.
**Root cause in spec:** §7 v1.0 named Microsoft/Alphabet as "benchmarks" but
supplied no values, while §1/§3 forbade external lookup — an internal
contradiction the executor resolved by inventing unsourced figures.
**Fix applied to spec:** §7 adds a **benchmark-sourcing rule** restricting
benchmarks to Apple's own FY2024 and the stated general norms, explicitly
barring peer ratio values and credit ratings; §9 bars unsourced external
evidence in recommendations.

### Issue 4 — Broken internal cross-reference
**What the LLM did:** Recommendation 3 contains "(Recommendation 3 in the Du
Pont driver analysis above)" — a self-referential pointer; it meant the Du Pont
driver discussion, not recommendation R3.
**Root cause in spec:** §9 v1.0 gave no cross-reference convention, so the
executor reused "Recommendation N" numbering for a section pointer.
**Fix applied to spec:** §9 adds a cross-reference rule — number recommendations
R1…Rn and cite other parts by section name, never by a bare "Recommendation N."

### Issue 5 — Length target unachievable
**What the LLM did:** Produced 3,165 words against the spec's "~1,200–1,800
words" cap — a 76% overshoot.
**Root cause in spec:** §10 v1.0's word ceiling was irreconcilable with its own
seven mandated sections (five ratio categories + Du Pont + 5 recommendations ×
(a)/(b)/(c) + validation table cannot fit 1,800 words).
**Fix applied to spec:** §10 raises the target to ~2,200–3,000 words and adds an
explicit compression-priority order for when length must be constrained.

## 4. Spec Changes (v1.0 → v1.1)

| Section | Change | Reason |
|---------|--------|--------|
| Header | Version 1.0 → 1.1 + changelog block | Track the HIL revision (Stage 4 rubric: visible iteration) |
| §3 Cash Flow | Replaced 2-line table with complete operating/investing/**financing**/net-change tables; values explicit | Issue 1 — executor had no financing or net-cash data to report |
| §3 Cash Flow | Added capex line (−$12,715M) + caution box (`CASH_investments` ≠ capex; FCF = op − \|capex\|) | Issue 2 — prevent the net-investing-as-capex error |
| §7 | Added required **Cash-Flow Analysis** bullet | Issue 1 — make the cash-flow narrative mandatory in output |
| §7 | Added benchmark-sourcing rule (no unsourced peer figures / ratings) | Issue 3 — remove the peer-benchmark vs. no-lookup contradiction |
| §9 | Added evidence-traceability + cross-reference (R1…Rn) convention | Issues 3–4 — kill unsourced evidence and the broken self-reference |
| §10 | Raised length to ~2,200–3,000 words; added compression-priority order | Issue 5 — reconcile target with mandated content |
| §10 | Added **Cash-Flow Analysis** as deliverable section 4 | Issue 1 — lock it into the required output structure |

## 5. Round-2 Result

v1.1 was not re-executed (this is an Option-3 annotated-diff submission, not an
Option-2 re-prompt). The v1.1 edits are nevertheless *compelling* rather than
merely *suggestive* — each forces a checkable change in executor behavior:

- The §3 financing/net-change tables mean a v1.1 executor **must** report the
  −$120,686M financing outflow, the −$90,711M buyback line, and the +$5,991M net
  cash change; absence is now a spec violation, not a data gap (fixes Issue 1).
- The §3 capex line + caution box make $98,767M the only spec-consistent FCF
  figure and make "FCF ≈ operating − CASH_investments" explicitly prohibited
  (fixes Issue 2).
- The §7 benchmark rule + §9 evidence rule make "Aaa/AA+" and "peers' current
  ratios" non-citable; an executor following the spec can no longer introduce
  them (fixes Issue 3).
- The §9 cross-reference convention makes "Recommendation 3 in the Du Pont
  analysis" malformed by rule (fixes Issue 4).
- The §10 raised ceiling removes the structural impossibility that produced the
  length overshoot (fixes Issue 5).

The features the v1.0 executor already handled well (Du Pont gap, ratio values,
validation checks, reclass disclosure) are untouched, so no regression surface
was introduced.

## 6. Reflection (150–200 words)

The most instructive failure was Issue 1: the executor did not "forget" the
financing activities — it never had them, because v1.0 silently equated *the
named ranges* with *the data*. The cash-flow tab held the full statement, but my
spec only surfaced two subtotals, so a faithful executor produced a faithful but
incomplete answer. Precision is not just stating numbers correctly; it is
auditing what the spec *omits* against what the deliverable *requires*. Issue 2
reinforced this: `CASH_investments` was present but its meaning (a net figure,
not capex) was not, and the model filled the gap with a plausible-but-wrong
proxy — and was nearly right by luck, which is the dangerous case. Issue 3
showed that a spec can be internally contradictory (forbid lookups, yet ask for
peer benchmarks) and the model will resolve the contradiction by inventing data
rather than flagging it. The lesson: specify the negative space — what *not* to
do, what a value is *not*, and what *must appear* — as explicitly as the
formulas. An LLM executor is literal exactly where a human colleague would ask a
clarifying question.
