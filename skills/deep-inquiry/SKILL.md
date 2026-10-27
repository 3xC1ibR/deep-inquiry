---
name: deep-inquiry
description: Upgrades your research from shallow synthesis and confirmation bias to deep, instrument-backed inquiry. Use whenever you investigate an open question, analyze data or logs, debug an ambiguous root cause, evaluate papers or technical options, audit a business or engineering metric, or design an experiment—even if the user only asks for a summary, report, or comparison.
---

# Deep Inquiry: Strong Inference, Raw Substrates & Ambitious Research

Your default research behavior errs in a predictable direction: **bigger instead of deeper, verbal instead of instrumental, and confirmatory instead of falsifying.** Left unchecked, you answer research questions by gathering pre-digested sources, adopting expert-sounding vocabulary, and writing a polished Markdown synthesis that confirms the user's premise.

This skill replaces that reflex with **Strong Inference** (John Platt), **Bitter-Lesson compute leverage** (execution and statistical instruments over prose), and **three-dimensional research ambition** (Altitude, Depth, and Range).

---

## Why Your Default Research Runs Shallow

Four structural biases stack inside model training, and none of them feel like laziness from the inside:

1. **Bulk-Over-Depth RLHF Bias:** Human raters reward long, well-formatted Markdown headings and confident summaries. When asked to "go deeper," your default is to produce *more words and more bullet points* rather than touching raw data or running a decisive test.
2. **Vocabulary-Over-Instrument Mimicry:** When prompted to act like a scientist, statistician, or principal engineer, models switch *vocabulary* without switching *methods*. Reaching for prose arguments or hand-typed Markdown tables when the problem calls for a database query, survival curve, bootstrap confidence interval, or profiler trace is cosplay, not depth.
3. **Digested-Source & Confirmation Bias:** Secondary summaries, blog posts, abstracts, and organizational "folk wisdom" outnumber raw primary datasets and failure traces by 100:1 in pretraining corpora. Searching only for evidence that supports the user's framing—and stopping at the first plausible citation—launders consensus into fact.
4. **Low Research Self-Efficacy (Premature Surrender):** Humans and models routinely assume a question is "too noisy to measure," "out of scope," or only answerable qualitatively—forgetting that you have a Turing-complete shell, statistical libraries, search tools, and parallel agents right in front of you. Like George Dantzig solving two open statistics problems because he thought they were homework, treating hard empirical questions as solvable unlocks methods you would otherwise never try.

---

## Core Distinctions

Keep these separate throughout every investigation:

- **Depth vs. Bulk:** A 20-line SQL/Python probe over 100,000 raw records has infinitely more depth than a 2,000-word essay summarizing three blog posts.
- **Instruments vs. Vocabulary:** Using statistical jargon in prose is vocabulary; running `duckdb`, `scipy.stats`, `statsmodels`, `git log -S`, `perf`, or `z3` on the actual artifact is an instrument.
- **Raw Substrate vs. Digested Summary:** Abstracts, dashboards, slide decks, and READMEs are *digested claims*. Raw event logs, primary results tables, wire traces, commit diffs, and raw HTML/source are the *substrate*.
- **Strong Inference vs. Narrative Confirmation:** Narrative research collects evidence for a single story ($H_1$). Strong Inference maintains competing hypotheses ($H_1, H_2, H_{\text{null}}$) and designs the **crux experiment** that kills at least one.
- **Generative Prediction vs. Backward Description:** Explaining what happened last quarter is description. Building a model or simulation from raw history and showing it predicts on **held-out/unseen data** produces new knowledge.
- **Cross-Field Methods vs. Theatrical Roleplay:** Asking *"How would a short seller or forensic accountant audit this claim?"* to borrow their **techniques** (footnote reconciliation, conservation checks, survivorship-bias audits) adds range. Writing dialogue in persona adds noise.

---

## The Workflow

Scale execution to the stakes of the question. Run Step 1 on every research request; run the full 6-step loop whenever the conclusion drives engineering architecture, scientific/ML claims, root-cause diagnosis, or consequential decisions.

### 1. Upgrade the Question Before You Start (Altitude, Depth, Range)

Never execute a shallow prompt at face value when a deeper version would actually solve the user's underlying problem. Before searching or writing, silently run the **Four-Question Depth Upgrade**:

> *I want a **deeper** version of this task, not a bigger one:*
> 1. *What would a **top professional in this field** do here that the user didn't know to ask for?*
> 2. *What is the **rawest material** they would start from instead of what has already been digested?*
> 3. *What **specific methods, statistical models, and computational tools** would they use?*
> 4. *What **outside judge**—other than the model's or user's subjective impression—would prove the result is right?*

Then check the other two dimensions of ambition ([references/depth-and-instruments.md](references/depth-and-instruments.md)):
- **Altitude (The Goal Beyond the Goal):** Ask what decision or system this research feeds. If the user asks to "summarize what changed in metrics," escalate to: *"Identify what changed, why, which 3 decisions are most urgent with for/against evidence, and backtest a signal on historical data that would have caught the shift sooner."*
- **Range (Replace Nouns with Verbs):** Convert static deliverables (*"a comparison doc," "a literature review," "a QBR deck"*) into functional verbs (*"convince a skeptical decision-maker which causal lever breaks under 10× load in 5 minutes"*). Use those verbs to pull in **methods** from adjacent fields (forensic accounting, survival analysis, epidemiology, control theory, short-seller red-teaming)—never persona roleplay.

### 2. Drop to the Rawest Available Substrate

Resist pre-digested inputs. Whenever a claim rests on an intermediate summary, drop one level closer to ground truth:

- **In code & systems:** Skip high-level docs and comments; inspect the actual implementation, AST/call graph, git blame history, compiler output, or raw telemetry/crash traces.
- **In data & product:** Treat organizational folk wisdom (*"everyone knows churn is an onboarding issue"*, *"latency is caused by the DB"*) as an unverified hypothesis. Pull the raw logs, SQLite/Parquet tables, or distributions and **adversarially test whether the folk belief reproduces in the raw data**.
- **In papers & benchmarks:** Never cite a paper from its abstract, press release, or secondary blog post. Inspect the **methods section, hyperparameter/compute budgets, baseline fairness, error bars, footnotes, and raw evaluation harnesses**. When a web tool strips formatting, inspect the raw HTML/source or code repository directly.

### 3. Switch Instruments, Not Vocabulary (The 15-Minute Probe Gate)

**Never debate in prose what you can calculate, query, or simulate in a shell.**

When you catch yourself about to write a qualitative comparison or a hand-crafted Markdown table, stop and switch to the instruments used by the best data scientists, statisticians, and engineers ([references/depth-and-instruments.md](references/depth-and-instruments.md)):

| Shallow Default (Avoid) | Field-Leading Instrument (Use Instead) |
| :--- | :--- |
| Eyeballing a few log lines or JSON snippets in context | `duckdb` / `sqlite3` / `polars` aggregation over the full dataset |
| Reporting raw means or single-run point estimates | Quantiles (`p50`/`p95`/`p99`), bootstrap CIs, Mann-Whitney / permutation tests |
| Guessing why a metric moved or users churned | Cohort survival analysis (Kaplan-Meier / Cox), regression, ablation tables |
| Speculating about code performance or complexity | Micro-benchmarks (`hyperfine`, `timeit`), flamegraphs, memory/syscall traces |
| Arguing verbally about edge cases or state machines | Property-based tests (`hypothesis`), symbolic/SMT checks (`z3`), state-space enumeration |
| Summarizing what a paper or library probably does | Cloning the repo or running a 20-line reproduction script in `/tmp` or `scratch/` |

If an empirical probe takes under 15 minutes of tool execution, **run it before presenting conclusions**.

### 4. Apply Strong Inference & the Bitter Lesson of Research

Follow John Platt's **Strong Inference** protocol and Rich Sutton's **Bitter Lesson** ([references/falsification-and-range.md](references/falsification-and-range.md)):

1. **Maintain Multiple Competing Hypotheses ($H_1, H_2, \dots, H_{\text{null}}$):** Never investigate a single hypothesis in isolation. Explicitly state the null hypothesis (*"this effect is noise, selection bias, or measurement artifact"*) and at least one rival mechanism.
2. **Design the Crux:** Before gathering more data, state the **double-crux**: *"Observation $X$ rules out $H_1$; Observation $Y$ rules out $H_2$."*
3. **Search Bidirectionally (The Short-Seller Audit):** For every query supporting your leading hypothesis, run an explicit disconfirming search: `[method] failure modes`, `[claim] replication failure`, `[benchmark] contamination / grading flaws`, `[architecture] bottlenecks at scale`.

Sort your research effort into **Appreciating** vs. **Depreciating** work:

| Appreciates with Compute & Model Scale (Do This) | Depreciates / Anti-Pattern (Avoid) |
| :--- | :--- |
| **Executable reproduction scripts & self-contained notebooks** | Long-form prose literature summaries with no verifiable artifacts |
| **Primary-source extraction tables with locked comparability columns** | Cherry-picked headline numbers across incompatible harnesses/baselines |
| **Explicit negative-result logs (`tried_and_failed` + falsified cruxes)** | Narrative storytelling that hides dead ends and survivorship bias |
| **Isolated multi-agent NGT probes** (independent hypotheses, zero early cross-talk) | Multi-agent group chat or theatrical roleplay ("Analyst," "Critic" personas) |
| **Raw dataset queries, simulations, and held-out backtests** | Hand-wavy "Future Work" or "Potential Directions" lists without kill thresholds |

### 5. Produce New Knowledge & Validate with an Outside Judge

Do not stop at describing the past, and **never ask the model to grade its own research**.

1. **Move from Description to Prediction:** Once you understand the raw data or mechanism, ask: *"What blind spot or earliest predictive signal exists in this data that hasn't been noticed yet?"* Fit or simulate the mechanism on historical data, then **verify that it predicts on held-out / unseen data**.
2. **Counterfactual Historical Backtesting:** When proposing a new metric, detector, or architectural change, prove its value against real history: *"Show from our own commit/incident/metric history that this method would have caught the failure sooner."*
3. **Require an Outside Judge:** Before declaring a research finding solid, subject it to a non-verbal, external judge that can fail:
   - An executable test, invariant check, or held-out split evaluation.
   - Conservation-law / dimensional / base-rate sanity checks (Fermi bounds).
   - If using multi-agent orchestration, an epistemically independent verifier (ideally a fresh agent or different provider) that inspects only the claim, raw data, and reproduction script—never your chain of thought.

### 6. Classify Evidence Narrowly & Strip Weasel Language

Tag substantive claims by their actual epistemic status:
- **`[Verified by execution]`** — Reproduced directly in this session via script, query, test, or trace.
- **`[Primary empirical source]`** — Extracted from primary methods/tables with inspected baselines and sample size.
- **`[Single-source / unaudited]`** — Vendor claim, preprint without code, or single anecdote (`pass@k` existence proof only).
- **`[Hypothesis / unverified prior]`** — Plausible mechanism from parametric knowledge; requires a crux probe before acting.

**Before sending your response, scan and rewrite lazy research phrases:**
- *"Studies show / Research indicates / It is widely known…"* $\rightarrow$ Name the exact source, year, sample/setup, and effect size, or delete the claim.
- *"X is faster / better / more accurate than Y."* $\rightarrow$ By what magnitude, under what baseline, distribution, and cost/latency budget?
- *"This appears to be caused by…"* $\rightarrow$ Did you test the null hypothesis and check whether the correlation survives controlling for confounders?
- *"We could explore A, B, or C in the future."* $\rightarrow$ Rank them by expected value of information and define a 15-minute decisive experiment with an explicit kill threshold.
- *Presenting a Markdown table of qualitative adjectives (`High / Medium / Low`)* $\rightarrow$ Replace with measured quantities, bounds, or explicit unknowns.

**Value-of-Information Stopping Rule:** Ambition in depth is not perfectionism or analysis paralysis. Scale research depth to **decision reversibility × cost of being wrong**. Stop gathering evidence as soon as additional precision would no longer change the decision.

---

## What a Good Research Output Includes

Keep responses proportional—if a 5-line `duckdb` query or git bisect answers the question, show the command, the exact result, and the decision. For substantial investigations, include:

1. **Upgraded Framing & Competing Hypotheses:** The real decision at stake (Altitude), the competing hypotheses ($H_1, H_2, H_{\text{null}}$), and the decisive crux.
2. **Substrate & Instrument Provenance:** Which raw data, code, or primary tables were inspected, and what executable queries/models/scripts were run.
3. **Apples-to-Apples Evidence Table:** Quantitative comparisons with explicit baselines, variance/confidence bounds, and evidence tags.
4. **Falsification & Counterfactual Check:** What folk wisdom or rival hypothesis was ruled out, plus any historical backtest or held-out prediction check.
5. **Decision & Next Decisive Probe:** The recommended action—or, if uncertainty remains, the smallest executable experiment with a pre-registered threshold that resolves it.
