---
template: prompt-log
purpose: "Running log of meaningful AI prompts and outputs used in a project — supports reproducibility and AI-use disclosure"
audience: student
fields_required: [date, goal, prompt, tool, output_location, notes]
naming_convention: "prompt-log.md (one per project, lives in deliverables/)"
courses: [BUS-629]
---

# Prompt Log

**Project:** BUS-629 Stage 4 — Apple Inc. (AAPL) Accounting & Performance Ratios · **Author:** Truc Pham

| Date | Goal | Exact Prompt | Tool (LLM/Sheet/Code) | Output Link/Location | Notes |
|------|------|--------------|------------------------|----------------------|-------|
| 2026-05-17 | Draft the Stage 4 technical specification for the Apple ratios model from the source materials | `Read these files: [stage4-technical-specification.md URL]; [spec-template.md URL]; models/templates/performance-ratios-template.xlsx; models/builds/<Stage 3 file>.xlsx. Draft a technical specification for {company} accounting ratios analysis, following the spec-template structure. Save it to docs/specs/<YYYY-MM-DD>-<lastname>-<company-slug>-spec.md` | Claude Code (Opus 4.7) | `docs/specs/2026-05-17-pham-apple-spec.md` (v1.0) | Fed the Stage 4 brief, spec-template, instructor template, and the Stage 3 workbook; extracted all inputs/formulas from the .xlsx named ranges. Flagged that the workbook uses the `_curr`/`_prior` suffix convention, not the template's example `_YYYY`. |
| 2026-05-17 | Test spec v1.0 by having a zero-context LLM execute it as the deliverable | `You are a financial analyst executor. Using ONLY the specification below, produce the deliverable it describes. Do not look up, infer, or estimate any figure not stated in the spec.` + full text of spec v1.0 | Claude Sonnet 4.6 (separate, zero-context conversation) | `2026-05-17-pham-apple-ratio-analysis_1.md` (3,165 words) | Round-1 executor run used as the HIL test input. Output was largely correct (Du Pont gap, ratio values, validation checks) but exposed five spec gaps. |
| 2026-05-17 | HIL iteration: review the executor output, identify spec gaps, fix the spec, and document an annotated diff | `'2026-05-17-pham-apple-ratio-analysis_1.md' read this outcome and Create analysis/validation/2026-05-17-pham-apple-stage4-iteration.md with this structure: [annotated-diff template]` — plus follow-up: `the cashflow statement from the output is still missing ... the financing breakdown and net increase/(decrease) in cash` | Claude Code (Opus 4.7) | `analysis/validation/2026-05-17-pham-apple-stage4-iteration.md`; `docs/specs/2026-05-17-pham-apple-spec.md` (v1.1) | Found 5 issues; cash-flow incompleteness was primary (user-identified). Spec revised v1.0→v1.1: complete Cash Flow Statement + capex caution, required Cash-Flow Analysis output section, benchmark-sourcing rule, cross-reference convention, reconciled length target. |
