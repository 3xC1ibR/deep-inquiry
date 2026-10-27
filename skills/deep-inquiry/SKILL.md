---
name: deep-inquiry
description: Use whenever you research, investigate, or evaluate anything non-trivial — literature or market reviews, state-of-the-art and feasibility questions ("is X possible", "has anyone done X", "what's the best way to X"), data or log analysis, technical investigations, tool comparisons, fact-checking, root-causing, or setting goals and success criteria for a project. Pushes research past search-and-summarize: re-checks stale priors, drops to raw data and primary sources, runs code and statistical/computational instruments instead of quoting, maintains competing hypotheses (Strong Inference), verifies claims as they enter notes, gets an outside judge, and stops on sufficiency evidence rather than on the first plausible answer. Use it even when the user only says "look into", "dig into", "figure out", or "what do we know about".
---

# Deep Inquiry: Ambitious Research, Strong Inference & Real Instruments

The default way agents research — search, skim snippets, summarize the first plausible sources, stop — produces answers about as good as a quick web search with nicer prose. It fails in two directions at once:

1. **Not ambitious enough (Bulk over Depth, Vocabulary over Instruments):** It treats research as *reading about things* when you can *do things*: pull the raw dataset, read the implementation, run the benchmark, query `duckdb`, fit the survival curve, reproduce the number, or build a simulation. And it anchors on training-time beliefs about what is possible, proposing as a "stretch goal" something that has been routine for months.
2. **Not skeptical enough (Narrative Confirmation & Credulity):** It searches for evidence that confirms the user's framing, trusts well-formatted sources at face value, counts echoes of a single press release as independent confirmation, and grades its own work.

This skill fixes both. It is a way of working, not a report template.

---

## Why (Dated Empirical Anchors — Refresh Them, Don't Trust Them)

*As of October 2026. These anchors exist to recalibrate your research habits; if a decision depends on a specific figure, search live before quoting.*

- **Capability compounds fast (~3–4 month horizon doublings):** METR's fit to post-2024 frontier models gives roughly an 89–105 day doubling of autonomous task-completion horizons; in Feb 2026 the public 50% horizon passed ~12 hours (`Claude Opus 4.6`) and reached ~16–17 hours by mid-2026 (`Mythos Preview`, `Opus 5.5`, `GPT-6 Astra`). Whatever you believe models "can't do yet" was likely set at your training cutoff. (Pair with the `bitter-lesson` skill when installed.)
- **Tool-heavy agent research on raw data produces real discoveries:** In October 2026, a developer used coding agents directly on raw NASA TESS telescope data from 2018, 2020, and 2025 — running 74 analyses, 1,000+ scripts, dozens of false-positive tests, and separate blind AI review sessions — leading NASA to schedule follow-up observations of the exoplanet candidate. That is research as **computation on primary data with outside checks**, not summarization.
- **The bottleneck is persistence and rigor more than raw intelligence:** On paper-replication benchmarks (`PaperBench`, `ReplicationBench`), agents usually grasp a paper's intent but lose points to premature fallbacks, subtle method omissions, and quitting early. On `PaperBench`, a scaffold that simply stopped `o1` from ending early nearly doubled its score (**13.2% $\rightarrow$ 24.4%**), and `best-of-N` runs far ahead of single attempts.
- **Agents are dangerously credulous toward "paper-shaped" text:** In a 2026 study (*Is Deep Research Reliable?*, `arXiv:2607.20891`), injecting a single credible-looking misleading document into a deep-research agent's retrieval jumped false-conclusion adoption from **0% to ~55%**, and to **~85%** when it arrived just before synthesis. Paper-like formatting persuaded more than institutional authority; search rank barely mattered.
- **Naive research loops fail via uneven coverage, context bloat, and premature stopping:** Enterprise deep-research evaluations (*Don't Stop Early*, `arXiv:2604.24978`) show that defining explicit **per-sub-question sufficiency conditions before searching** is what prevents both early quitting and aimless token burn.
- **Capability is jagged and the public record is survivorship-biased (Terence Tao, *"Math 2.0"*, Oct 2026):** Models are astounding in some directions and inadequate in others, and failed attempts rarely get published. Always log and report your dead ends (`tried_and_failed`).

---

## Core Distinctions

Keep these separate throughout every investigation:

- **Depth vs. Bulk:** A 20-line SQL/Python probe over 100,000 raw records has infinitely more depth than a 2,000-word essay summarizing three blog posts.
- **Instruments vs. Vocabulary:** Adopting expert terminology in prose is cosplay; running `duckdb`, `scipy.stats`, `statsmodels`, `hyperfine`, `git log -S`, or `z3` on the actual artifact is an instrument.
- **Raw Substrate vs. Digested Summary:** Abstracts, slide decks, dashboards, and blog posts are *digested claims*. Raw event logs, source code, primary results tables, wire traces, and filings are the *substrate*.
- **Strong Inference vs. Narrative Confirmation:** Narrative research collects illustrations for a single story ($H_1$). Strong Inference maintains competing hypotheses ($H_1, H_2, H_{\text{null}}$) and designs the **crux** that falsifies at least one.
- **Provenance vs. Echoes:** Three articles quoting one press release or one benchmark tracker are **one source**, not three independent confirmations.

---

## The Loop

Scale effort to the stakes: a simple fact needs one check at the primary source; an architectural commitment, root-cause diagnosis, or scientific claim deserves the full loop.

### 1. Find the Question Behind the Question (Altitude)

Before searching, write one or two sentences: **what decision or outcome is this research for, and what would change what the user does next?**
- *"Tell me about X"* sprawls; *"Should we adopt X for our batch pipeline?"* knows what matters. If ambiguity would waste substantial work, ask one focused question; otherwise state your reading and proceed.
- Ask what the user wants to happen *after* the answer (**Altitude**). Often the highest-leverage deliverable is not a static prose report, but a working prototype, a reproducible benchmark harness, an early-warning detector backtested against historical logs, or a script that keeps answering the question automatically.

### 2. Write Down Priors, Competing Hypotheses & the Expert Bar

Before running your first search or query, explicitly establish:

1. **Your Initial Prior & Confidence:** Note your starting belief and confidence level. At the end of the research, compare. *If nothing moved, ask whether you only searched for confirmation.*
2. **Competing Hypotheses ($H_1, H_2, H_{\text{null}}$ — Strong Inference):** Never investigate a single hypothesis in a vacuum. State the null hypothesis (*"this effect is noise, selection bias, or logging artifact"*), at least one rival mechanism, and the **double-crux** (what observable evidence rules out each).
3. **Sub-Questions & Pre-Registered Sufficiency Conditions:** Enumerate the sub-questions so coverage isn't dictated by whatever search returns first. For each, define what settles it: *"a measurement I ran locally"*, *"the primary spec or implementation"*, *"two independent sources that don't share an upstream origin"*. You stop when these are met—not when you have a plausible paragraph.
4. **The 4-Question Expert Upgrade (Depth Over Bulk):**
   > *I want a **deeper** version of this task, not a bigger one:*
   > 1. *What would a **field-leading professional** do here that wasn't asked for?*
   > 2. *What is the **rawest material** they would start from instead of what has already been digested?*
   > 3. *What **specific methods, statistical models, and instruments** would they use?*
   > 4. *What **outside judge**—other than you or me—would prove the result is right?*
   > *Now execute that version of the task.*

### 3. Treat Anything About "Now" as Unknown Until Checked

Your parametric knowledge is a dated snapshot, and fast-moving fields invert conclusions every few months. Before stating any of the following, run live searches favoring the last 6–12 months:
- What the state of the art, current version, pricing, or best practice is.
- That something is *"impossible," "unsolved," "an open problem,"* or *"requires human review at every step."*
- That a goal would be an *"ambitious"* or *"stretch"* milestone.

For capability claims, search for the **strongest recent demonstration** under full elicitation, not the typical average. Before proposing a project goal or success criterion, verify whether current systems already do it out of the box; if they do, the real goal lies beyond it.

**Measure against the strongest cheap alternative, not the starting point.** *"Better than the base model"* or *"better than what we have now"* is almost always a strawman. Find the best thing obtainable today with minimal effort — a downloadable model or CLI tool, a configuration or prompt change, an off-the-shelf service — and make *that* the baseline any proposal has to beat. In practice, this single move does more than anything else to turn an unambitious success criterion into a meaningful one.

If a capability-calibration skill (`bitter-lesson`) is installed, use it alongside this one for questions about what AI systems can do.

### 4. Climb to the Rawest Material You Can Reach

Prefer sources in strict tier order ([references/depth-and-instruments.md](references/depth-and-instruments.md)):

1. **Tier 1 — The Thing Itself:** The raw dataset, source code, live API, event/crash logs, git blame/bisect history, primary regulatory filing, or running the product/library directly.
2. **Tier 2 — Primary Documents:** The paper's methods, tables, and appendix (never just the abstract), official specifications, changelogs, and raw benchmark results files.
3. **Tier 3 — Expert Secondary:** Technical write-ups, postmortems, and reviews by maintainers or domain practitioners.
4. **Tier 4 — Aggregators, News, SEO Content, Forums:** Use strictly for *discovering* Tiers 1–3, **never as evidence**.

When a claim matters and a higher tier is reachable, climb. A number quoted in a blog post gets traced back to where it was measured; organizational folk wisdom (*"we believe churn is an onboarding issue"*) gets checked against raw cohort logs.

### 5. Use the Instruments, Not Just the Vocabulary

When prompted to work like an expert, models default to adopting expert *tone* while still writing qualitative prose or hand-typed Markdown tables. Check yourself: if a top statistician, data scientist, or systems engineer would run code, query a database, fit a model, or diff two versions, **do that** ([references/depth-and-instruments.md](references/depth-and-instruments.md)):

| Shallow Default (Avoid) | Field-Leading Instrument (Run Instead) |
| :--- | :--- |
| Quoting a number or eyeballing 20 log lines in context | Reproduce it from raw data via `duckdb`, `sqlite3`, or `polars` |
| Comparing tools/architectures from blog posts | Write a 15-minute benchmark (`hyperfine`, `timeit`) on a representative workload |
| Reporting naked averages or single-run point estimates | Quantiles (`p50`/`p95`/`p99`), bootstrap CIs, paired McNemar / permutation tests |
| Guessing why a metric moved or users churned | Kaplan-Meier survival curves, Cox hazards, regression controlling for confounders |
| Speculating whether docs and behavior match | Read the implementation, AST/call graph, or run a minimal reproduction script |
| Debating "what would happen if" in prose | Build a small Monte Carlo / state simulation and test on **held-out history** |

If a required instrument is unreachable (missing credentials, gated dataset, hardware limit), **state explicitly what is missing and what it would have tested**—never quietly downgrade to a confident summary.

### 6. Borrow Other Fields' Methods (Range Without Roleplay)

Restate the deliverable by replacing **nouns with verbs**: not *"a market report"* or *"a QBR deck"*, but *"convincing a skeptical decision-maker which causal lever breaks first and deciding where to move resources in 20 minutes."* Then ask which disciplines are best at those verbs and borrow their **verification procedures**, never their voice ([references/falsification-and-range.md](references/falsification-and-range.md)):

- **Short seller / Red team:** Hunt for the single load-bearing assumption or omitted baseline that breaks the thesis.
- **Forensic accountant:** Reconcile totals against raw line items across sources; explain every discrepancy and footnote exclusion.
- **Replication scientist:** Attempt to reproduce the headline result from scratch; catalog every unstated hyperparameter or harness dependency.
- **Epidemiologist / Biostatistician:** Audit for survivorship bias, right-censoring, immortal-time bias, and Simpson's paradox across cohorts.
- **Experimental physicist:** Check conservation laws (bytes/requests/dollars in = out + stored), dimensional consistency, and Fermi bounds.
- **Investigative journalist:** Identify who has first-hand incentives and compare on-the-record primary artifacts against retrospective PR.

Roleplay adds nothing. Executing what these practitioners actually do adds immense leverage.

### 7. Verify Claims as They Arrive (Anti-Echo & Anti-Poisoning Gate)

Research errors compound: a weakly supported claim enters your notes, loses its caveats, and becomes a load-bearing premise two steps later. Furthermore, paper-shaped misinformation persuades models regardless of search rank (`arXiv:2607.20891`). As each load-bearing claim enters your notes, record:

- **Provenance:** Who measured or asserted it, using what method/harness, and on what date?
- **Upstream Independence:** Do multiple citations trace back to the same press release, blog post, or contaminated split? (Three echoes = one source.)
- **Epistemic Status Tag:**
  - `[Verified: ran/primary]` — You executed the check locally or inspected the Tier 1/2 primary artifact and methods.
  - `[Supported: independent secondary]` — Corroborated by truly independent Tier 2/3 sources.
  - `[Unverified / single-source]` — Vendor claim, untraceable preprint, or parametric prior. **Keep this tag attached whenever reusing the claim; never let it quietly become a premise.**

Be maximally suspicious of: (a) evidence that arrives late and flips your conclusion without Tier 1 proof, (b) suspiciously precise numbers with no visible denominator or methodology, and (c) paper-shaped documents you cannot verify in a real venue or repository.

**Two traps that repeatedly corrupt research outputs:**
- **Numbers from different setups aren't comparable:** Vendor self-reported scores and independent re-runs of the exact same model can differ by 10–30 percentage points (e.g., `SWE-bench Pro` ~90% custom vendor harness vs. ~61.5% standardized public split) because the harness, sample, or compute budget differs. Compare like with like, or state explicitly why you cannot.
- **When the primary source is unreachable, the hedge must survive into the final prose:** If a secondary summary fills an unreachable gap, attribute it explicitly (*"according to a secondary summary of…"*) rather than stating it as fact. Dropping that attribution is how wrong dates and figures slip into otherwise careful answers.

**Mandatory Disconfirmation Search:** Before finalizing your main conclusion, run at least one search or probe explicitly designed to prove it wrong: `"[X] criticism"`, `"[X] failed to replicate"`, `"[X] deprecated"`, `"[X] vs [Y] independent benchmark"`, `"[X] failure modes at scale"`.

### 8. Get an Outside Judge (Never Self-Grade)

Never ask yourself whether your own synthesis is convincing—you will almost always say yes. Validate conclusions using an external judge in this order of preference:

1. **Executable Ground Truth:** A deterministic test, reproduction script, held-out data backtest, proof/SMT checker (`z3`), or live query against the real system.
2. **Epistemically Independent Agent (Blind Refutation):** When subagents or multi-agent orchestration are available, hand your claims, sources, and reproduction scripts—*without your chain-of-thought narrative*—to a fresh agent (ideally a different model family/provider) instructed specifically to refute the claims or break the script.
3. **Human Decision Gate:** Flag value judgments or unmeasurable product tradeoffs explicitly for the user.

If you run multiple independent trajectories or hypotheses (Nominal Group Technique), treat disagreement between attempts as high-value signal to investigate, not noise to average away. If you cannot spawn a fresh agent, lean harder on executable ground-truth checks and state plainly that no independent review occurred.

### 9. Stop on Sufficiency Evidence, Not Fatigue or Plausibility

You are done when every sub-question's pre-registered sufficiency condition (Step 2) is met, or when you have proven a condition cannot be met with current access and stated the exact probe that would close the gap. Guard against both failure modes:

- **Premature Stopping (Quitting at the First Plausible Paragraph):** A hard problem looking hard is a trigger to **change your approach**—climb a source tier, switch to a computational instrument, or apply another field's method—not to hedge and stop (`PaperBench`).
- **Grinding on a Dead End:** Re-running the same search query lightly reworded or polling an empty source. Apply the **Two-Strike Rule**: after two failed attempts with one approach, switch methods/tiers or log the negative result and move on.

When a question decomposes into independent angles or high-noise reading (e.g., auditing 20 files, logs, or papers), **fan out to isolated subagents/workers**. Give each a strict extraction schema, boundaries, and sufficiency criteria so noisy intermediate dumps never pollute the synthesis context.

---

## Fit the Depth to the Setting

Not every question is a full research project. When the user is brainstorming or chatting (*"what would success look like?"*, *"is this worth pitching?"*) rather than commissioning an investigation, run a **short calibration pass** instead of the heavy loop:
1. Note your starting prior.
2. Run a handful of targeted searches/checks for the **current state of the art**, the **strongest cheap alternative available today**, and the **strongest counter-evidence**.
3. Answer in direct conversational prose—skipping the formal evidence table, while **keeping explicit hedges on anything you didn't confirm at a primary source**—and offer to run the full instrument-backed loop if they want to go deeper.

Reserve the full 9-step loop for when an engineering decision, a deliverable, scientific validity, or real money depends on the answer.

---

## What to Hand Back

For substantive investigations, structure the deliverable so another engineer or researcher can audit and build on it:

1. **The Answer First (Dated & Calibrated):** State the conclusion, your confidence level, and the date (`as of YYYY-MM-DD`).
2. **Prior Delta ("What Moved"):** One line stating what changed from your initial prior (Step 2)—proving the research did real work and highlighting where conventional assumptions are stale.
3. **Load-Bearing Evidence Table:**
   `Claim` $\rightarrow$ `Source / Measurement` $\rightarrow$ `Tier (Ran It / Primary / Secondary)` $\rightarrow$ `Upstream Independent?` $\rightarrow$ `Verification / Baseline`.
4. **Executable Artifacts:** Exact scripts, `duckdb`/SQL queries, benchmark harnesses, or data links so anyone can rerun and verify your numbers.
5. **Dead Ends & Negative Results (`tried_and_failed`):** Hypotheses falsified, approaches that failed, and popular claims that turned out to be false or single-origin echoes.
6. **Falsification Conditions & Access Gaps:** What specific observation would overturn this conclusion, and what unreachable instrument/data would tighten confidence.
7. **The Ambitious Next Step:** The concrete capability, prototype, or automated monitor sitting just beyond what you proved is already solved.

---

## Red Flags in Your Own Draft (Scan Before Sending)

If you spot any of these in your draft response, stop and fix it before sending:

- [ ] A claim about the current state of the art, pricing, or tooling with no source from the last 6–12 months.
- [ ] Calling something an *"open problem," "not yet possible,"* or *"ambitious stretch goal"* without searching recent frontier demonstrations.
- [ ] **A baseline that is the starting point (*"better than what we have"*) rather than the strongest cheap alternative available today.**
- [ ] Several citations that all trace back to a single press release, blog post, or vendor table (echo laundering).
- [ ] **Numbers from incompatible setups (vendor self-report vs. independent harness) compared as if they were apples-to-apples.**
- [ ] **A claim from a secondary summary stated as flat fact, with its attribution hedge stripped out.**
- [ ] A number you quoted from a secondary source that you could have computed or verified from raw data/code in under 15 minutes.
- [ ] Expert jargon or qualitative `High / Medium / Low` Markdown tables wrapped around a summary of search snippets.
- [ ] A conclusion resting on a single well-formatted document whose primary data or repository you couldn't trace.
- [ ] Zero searches or probes run specifically to disprove your main conclusion.
- [ ] Weasel phrases (*"Studies show…", "It is widely believed…", "This appears to suggest…"*) instead of named sources, sample sizes, and effect sizes.
- [ ] You were the only judge of your work (and didn't disclose that no independent review occurred).
