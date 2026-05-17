# BUS-629 International Corporate Finance Project
## Apple Inc. (NASDAQ: AAPL) — Accounting & Performance Ratios Analysis

**Student:** Truc Pham
**Program:** MBA in International Corporate Finance, University of Hawaiʻi at Mānoa
**Course:** BUS-629 VEMBA | Instructor: Adam Stauffer

---

## What you'll find here

This repository is a spec-driven financial-analysis capstone on Apple Inc. (FY2025, 10-K). It works through a five-stage pipeline: select a company, populate a three-statement Excel ratio model, write a precise technical specification, have an LLM execute that specification cold, then manually verify, evaluate, and correct the output into a defensible final analysis. The core idea under test is that *specifying* analytical work precisely is more valuable than executing it — every numeric result traces back to the Stage 3 workbook, and every AI session is disclosed in the prompt log.

**Company:** Apple Inc. (NASDAQ: AAPL) · **Fiscal Year:** FY2025 (ended Sep 27, 2025) vs. FY2024
**Analysis focus:** Performance, Profitability, Efficiency, Leverage, Liquidity, and Du Pont decomposition

## Repository structure

- **`docs/decisions/`** — Stage 2 company-selection memo (+ any feedback responses)
- **`docs/specs/`** — Stage 4 technical specification (v1.1)
- **`docs/templates/`**, **`docs/plans/`** — template pointers and planning scratch
- **`models/templates/`** — instructor performance-ratios template (Stage 1)
- **`models/builds/`** — Stage 3 populated workbook (source of truth for all figures)
- **`analysis/validation/`** — Stage 4 HIL iteration + Stage 5 manual verification
- **`deliverables/`** — raw LLM output, final analysis, spec retrospective, prompt log
- **`data/`** — source-data scaffold

## Project status

| Stage | Description | Key commit | Status |
|-------|-------------|------------|--------|
| 0 | Repository setup | `2425e18` | Complete |
| 1 | Template architecture (instructor template + .gitignore) | `36f04aa` | Complete |
| 2 | Company-selection memo — Apple Inc. (AAPL) | `539dc3e` | Complete |
| 3 | Model population & validation (FY2025 workbook) | `286047e` | Complete |
| 4 | Technical specification (v1.0 → v1.1 after HIL iteration) | `1c7329e` → `0efcacf` | Complete |
| 5 | LLM analysis, verification, evaluation & repo polish | `b962f8e`, `2b81576`, `077e61b`, `dc411d7` | In progress |

## Getting started

1. `docs/decisions/` — why Apple was selected
2. `models/builds/` — the populated FY2025 ratio workbook
3. `docs/specs/` — the Stage 4 specification that drives the analysis
4. `deliverables/` — raw LLM output → final evaluated analysis → spec retrospective
5. `analysis/validation/` — manual ratio recomputation cross-check
6. `deliverables/prompt-log.md` — disclosure of every meaningful AI session

---

*Last updated: May 2026 · Licensed under the MIT License (see `LICENSE`).*
