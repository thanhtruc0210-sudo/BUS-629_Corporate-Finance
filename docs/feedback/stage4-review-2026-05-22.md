# Stage 4 review — 2026-05-22

Reviewing `docs/specs/2026-05-17-pham-apple-spec.md` and `deliverables/prompt-log.md`.

Truc — this is one of the strongest Stage 4 specs in the cohort, and what makes it stand out is *not* coverage (every spec hits the rubric items) but the engineering instincts behind the writing. Three things in particular: (1) the v1.0 → v1.1 changelog at the top of the spec, where you ran a zero-context executor against your own draft, found five gaps, and revised the spec before submission — that's a HIL methodology most students don't even know to attempt; (2) the inline **`CASH_investments` is not capex** caution callout in §3, which preempts a specific arithmetic mistake (using a net investing total as a capex proxy) by naming it before any executor can make it; and (3) the **benchmark-sourcing rule** in §7 that bars external peer ratios, credit ratings, and rating-agency grades from appearing as evidence — that's constraint-engineering, the same move a senior reviewer makes when they write "no unsourced figures" into a research mandate. The notes below are not "you need to fix this" — they're four directions you could take *next*, picked because they extend something you've already done well rather than papering over something missing. Take any one of them seriously and you're doing real AI-quant work, not student work.

---

## What the auto-scan confirms

| Signal | Value | Read |
|---|---|---|
| Section coverage | 10/10 (canonical 11 consolidated to 10 — reclassifications folded into §3/Notes) | Complete |
| Spec length | ~3,005 words | Above the 1,500–2,500 target band, justified by the v1.1 length-target reconciliation note in §10 |
| Named-range hits | 294 | Spec speaks the model's language at every level |
| Ratio categories in §5 | 6/6 (Performance, Profitability, Efficiency, Leverage, Liquidity, Du Pont) | ~29 rows in named-range notation |
| Validation rules | 7 | Each with the expected resolved value; V3 (Du Pont ROE time-mismatch as expected-not-an-error) and V7 (US-GAAP reclassification disclosure) are genuinely thoughtful |
| Prompt log | ~7 entries spanning Stage 4 + Stage 5 | Documents the v1.0 → v1.1 HIL iteration, the zero-context Stage 5 cold-session protocol, and a manual five-ratio cross-check |
| Distinctive moves | `CASH_investments`-is-not-capex caution; benchmark-sourcing rule; `IFERROR` guard for zero interest expense | Each preempts a specific failure mode rather than describing the happy path |

There is no Stage 4 rubric item where this spec falls short. The rest of this file is forward-looking.

---

## Four directions you could take next

These are ordered by how much new skill they exercise, not by priority — pick whichever interests you. None of them affects your Stage 4 score; this is intellectual extension work that the cohort's strongest students should be doing if they want their portfolios to actually demonstrate AI-quant capability rather than just "I followed the rubric."

### 1. Turn your spec into an eval harness (the "specification as benchmark" move)

You already have most of the pieces. Your Stage 5 verification file manually cross-checks five LLM-reported ratios against the workbook by hand. Your seven validation rules in §6 define what "right" means with explicit resolved values. The natural follow-up: if the spec is the prompt and the validation rules are the answer key, then the spec **is** an evaluation harness — you just haven't automated it yet.

**Concrete next step.** Take your Stage 5 raw LLM output (`deliverables/2026-05-17-pham-apple-llm-raw.md`) and write a 30-line Python script that:

- Reads the raw output Markdown.
- Extracts each ratio value the LLM reported (regex against the ratio tables is enough).
- Recomputes the expected value from your Stage 3 workbook using the named ranges in §4 / §5.
- Reports a pass/fail per validation rule (V1 balance-sheet check; V2 Du Pont ROA identity; V3 Du Pont ROE gap-explained-not-equality; V4 no `#REF!`/`#DIV/0!`; V5 prior-year populated; V6 sign sanity; V7 reclass disclosure).

You'd be the first student in the cohort to ship a spec with a programmatic conformance check attached. The artifact takes a few hours and demonstrates something most MBA finance courses don't even ask for: that you can specify a thing precisely enough to **grade** an AI's execution of it. Bonus: V3 is the interesting validation rule to encode, because pass means "the gap is explained in the narrative" — that's an LLM-judged check, which is itself a portfolio-worthy artifact.

### 2. Run the spec through three LLMs and write the diff

Right now your Stage 5 evaluates a single LLM's output (Opus 4.7, cold session) against your spec. The more interesting question — and the one that's harder to get a clean answer to — is: **how much does the model matter when the spec is good enough?**

**Concrete next step.** Take your finalized v1.1 spec, feed it to Claude (Opus), ChatGPT (GPT-4 or GPT-5), and Gemini Pro with the same wrapper prompt you already used for the cold-session run (literally: *"Read this spec and produce the analysis it requests. CRITICAL RULES: use only this spec as input; no web search; no training-data reference to AAPL beyond the spec; treat the spec as sole source of truth."*). Save all three outputs. Then write a one-page comparison:

- **Convergence:** Which ratio values do all three models compute identically? (These are the parts of your spec where the formula notation is unambiguous — likely the named-range-driven ratios.)
- **Divergence:** Where do they differ — in computed values, in narrative judgment, in how they handle the `n/a (no interest exp.)` cases, in how they explain the Du Pont ROE gap, in whether they obey the benchmark-sourcing rule? Almost always: the ambiguous parts of your spec, which then become a v1.2 revision target.
- **One-paragraph thesis:** What does the divergence pattern tell you about which parts of finance work are now commodity-AI tasks vs. which still need a human?

This is the genre of work being published in industry blogs (Anthropic, OpenAI, McKinsey AI practice) right now. A solid one-page version of it from a finance MBA student is a portfolio piece, not coursework. Given that your prompt log already shows you running the spec across two model versions (Sonnet 4.6 in the HIL test, Opus 4.7 in the cold-session run), you're 40% of the way there.

### 3. Sensitivity & Monte Carlo on the assumptions

Your spec uses two hardcoded analyst assumptions: `cost_capital = 8.5%` and `tax_rate = 15.6%` (FY2025 effective). Both are point estimates. EVA depends on `cost_capital` directly through the capital charge; after-tax operating income depends on `tax_rate` through the interest-tax-shield term (currently zero for AAPL because interest expense is zero, but the formula is sensitive in the general case).

A point-estimate spec produces a point-estimate analysis. A spec that **builds uncertainty in** produces an analysis that distinguishes "Apple's EVA is $99.9B" from "Apple's EVA is $99.9B ± $11B at 80% confidence, with the bulk of the uncertainty coming from WACC, not operating performance." Given how large Apple's capital base is, even a 100-bp move in `cost_capital` shifts the EVA capital charge by ~$1.4B.

**Concrete next step.** Add a §11 ("Sensitivity Specification") to your spec that defines:

```markdown
### 11. Sensitivity Specification

The Stage 5 analysis must include a one-page sensitivity appendix
covering the two assumption inputs:

| Input | Point estimate | Range to test | Distribution shape |
|---|---|---|---|
| cost_capital | 8.50% | 6.5% – 10.5% | Triangular, mode at 8.5% |
| tax_rate | 15.60% | 13.0% – 21.0% | Uniform |

Required outputs:
- One tornado chart showing which input moves EVA the most.
- A 5,000-trial Monte Carlo histogram of EVA with the 10th/50th/90th
  percentile values reported.
- One narrative paragraph: at what value of cost_capital does
  EVA cross zero? (For Apple, this is genuinely interesting because
  the answer is likely north of 60%, which itself is a finding.)
```

The Stage 5 LLM can produce this if your spec asks for it. The deliverable becomes a meaningfully better-than-textbook analysis — one that names what you don't know as well as what you do.

### 4. Spec-driven generalization — make the spec MSFT-runnable

Your spec is AAPL-specific in two places: §3 (data values) and the §6/V7 reclassification disclosure (which lists the specific Apple US-GAAP reclasses — PP&E net only, no goodwill/intangibles, current marketable securities folded into cash, AR + vendor non-trade receivables combined, deferred revenue into other current liabilities, commercial paper + current term debt into short-term debt, accumulated deficit + AOCI into retained earnings). The structure of §1, §2, §4, §5, §7 (analysis), §8 (Du Pont), §9 (recommendations), and §10 (output format) is **company-agnostic**. The deeper observation: a well-written spec should be a parameterized template, and the company-specific values and reclass list should be an appendix you swap out.

**Concrete next step.** Refactor the spec into two files:

- `spec-template.md` — the structure, with `{{COMPANY}}`, `{{TICKER}}`, `{{REPORTING_STANDARD}}`, `{{FISCAL_PERIOD}}`, and a `§3 placeholder` table for the inputs, plus a `§6 V7 placeholder` for the reclass-disclosure list.
- `2026-05-17-pham-apple-inputs.yaml` (or `.md`) — the AAPL-specific values in §3, the assumption set, and the specific reclassifications.

Then write a 1-paragraph note: *"To run this spec for Microsoft (MSFT) or any other large-cap with similar GAAP structure, replace the inputs file and re-run Stage 5. The analysis framework, validation rules, Du Pont decomposition, and benchmark-sourcing rule are unchanged."*

You will have shipped a **reusable analytical artifact** rather than a one-off deliverable. That's the difference between an MBA project and something you'd put on a senior analyst's GitHub. The fact that your spec already calls out which reclasses are Apple-specific (V7) makes this refactor cheaper than it would be for most students — you've already identified the parameterizable parts; you just haven't separated them yet.

---

## A small honest reaction to the prompt log

Your prompt log is the most procedurally rigorous in the cohort — six entries spanning Stage 4 draft → zero-context executor test → HIL iteration → Stage 5 cold-session protocol → manual five-ratio cross-check → evaluated final → spec retrospective. The two moves that stand out: (a) explicitly using a *separate, zero-context Claude Sonnet 4.6 conversation* to test spec v1.0, which is the right experimental design — you can't validate a spec by asking the same session that wrote it; and (b) running the Stage 5 executor in an *incognito tab with no projects, no memory* to control for context bleed-through. Most professionals don't run their spec evaluations with that much methodological hygiene.

The single way the prompt log could be sharper: the column where you capture the **prompt-as-written vs. prompt-as-it-should-have-been** is implicit in the row for Stage 4 (the v1.0 prompt fed templates by URL; v1.1 essentially fed the spec itself), but you don't surface it as a finding. Adding a one-paragraph "what I learned about prompt design across the seven entries" at the bottom — something like *"Stage 4 taught me that prompts referencing files outside the LLM's read access produce shallow output; Stage 5 taught me that a specification with explicit edge-case rules outperforms a conversational directive even when both reference the same workbook"* — would close the loop and turn the prompt log itself into a methodology artifact rather than a record.

---

## Looking ahead to Stage 5

Stage 5 will grade how cleanly your Stage 1–4 work coheres into a single deliverable. Yours already does — and you've already shipped it (`deliverables/2026-05-17-pham-apple-final-analysis.md`, 3,747 words, plus the spec retrospective). There is no Stage 5 cleanup work to schedule. Use that bandwidth on one of the four directions above instead. If you do, drop a note in your prompt log or under `analysis/explorations/` so the work is visible; if you don't, your Stage 5 will still come in clean on the rubric and you'll have lost nothing.

The post-deadline revision-sweep window is open if you want to add any of the above to the spec retroactively — bumps to Stage 4 are possible, though they're not the point. The point is whether one of these directions sounds interesting enough to spend a Saturday morning on. If yes, that's a much better use of the next two weeks than incremental polish on what's already a strong artifact. Direction 1 (eval harness) is closest to your current artifact set and would extend the manual five-ratio verification you already did into something that runs in 30 seconds; Direction 4 (generalization) is the highest-leverage portfolio piece if you want to demonstrate that the spec is reusable infrastructure rather than a one-off.

---

*This review is feedback-only — no scores included.* Score numbers live in the internal grade report and the instructor's email; this file is intended as colleague-level input on your work, not as a graded artifact.
