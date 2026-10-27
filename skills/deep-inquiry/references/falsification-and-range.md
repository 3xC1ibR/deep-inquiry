# Strong Inference, Falsification & Cross-Disciplinary Range Playbook

Use this playbook to prevent confirmation bias, single-hypothesis storytelling, and sycophantic multi-agent convergence.

---

## 1. John Platt's Strong Inference Protocol

In 1964, physicist John R. Platt asked why certain fields (molecular biology, high-energy physics) progressed orders of magnitude faster than others. The difference was **Strong Inference**—a systematic method of inductive reasoning applied at every step:

1. **Deconstruct & Formulate Alternative Hypotheses ($H_1, H_2, \dots, H_k, H_{\text{null}}$):**
   Never allow a single hypothesis to occupy the workspace alone. Always include:
   - $H_{\text{null}}$: The observed pattern is noise, sampling bias, survivorship bias, or a measurement/logging artifact.
   - $H_{\text{rival}}$: At least one competing causal mechanism that explains the same surface symptoms (including reverse causality or a common confounder).
2. **Devise the Crucial Experiment (The Double-Crux):**
   Before running queries or writing code, state explicitly:
   > *"If we observe $X$, $H_1$ is falsified. If we observe $Y$, $H_2$ is falsified."*
   If every possible outcome of your planned investigation is compatible with your hypothesis, **you are not doing research—you are collecting illustrations.**
3. **Carry Out the Probe Cleanly:**
   Execute the query, benchmark, or primary-source extraction so the result is unambiguous.
4. **Recycle the Procedure:**
   Record falsified hypotheses in `tried_and_failed` (negative memory), refine the surviving hypothesis into sub-hypotheses, and repeat until the decision threshold is met.

---

## 2. Bidirectional & Adversarial Search Templates

When researching literature, tools, architectures, or market claims, never run only positive-capability or confirmatory queries. Pair every constructive query with an **Adversarial Audit Query**:

### Constructive Discovery (Upper-Bound Search)
- `[problem / task] state of the art benchmark [year]`
- `[method / system] technical report architecture implementation`
- `[phenomenon] causal mechanism empirical study dataset`
- `[problem] mathematical formulation exact solver`

### Adversarial Discovery (Short-Seller / Falsification Search)
- `[method / paper] replication failure critique limitations`
- `[benchmark / metric] gaming contamination Goodhart flaws`
- `[technology / library] production postmortem bottleneck scale limits`
- `[claim] null result negative findings counterexample`
- `[vendor headline] independent benchmark apples-to-apples baseline`

**Null-Search Rule:** A search that returns no results is *absence of indexed phrasing*, not proof that something is impossible or novel. Broaden terminology across adjacent disciplines (Section 4) and run a local empirical probe before claiming a gap.

---

## 3. Comparable Evidence Extraction Schema

Never compare two papers, systems, or business cohorts using headline numbers alone. Extract a normalized table across these seven locked columns:

| Dimension | What to Audit Before Comparing |
| :--- | :--- |
| **1. Primary Artifact** | Did we inspect the raw data/code/methods table, or only a secondary summary/abstract? |
| **2. Baseline Parity** | Was the baseline tuned with the same compute, hyperparameter sweeps, and prompt/harness effort as the proposed method? |
| **3. Sample & Distribution** | Sample size ($N$), dataset split, tail difficulty, and whether easy/contaminated items dominate the average. |
| **4. Metric & Aggregation** | Mean vs. median/`p99`, `pass@1` vs. `pass@k`, absolute vs. relative lift (watch for big relative % on tiny base rates). |
| **5. Variance & Uncertainty** | Confidence intervals, standard error across seeds/runs, and statistical significance after multiple-testing correction. |
| **6. Resource / Unit Economics** | Wall-clock latency, memory footprint, token/compute cost, and operational complexity required to achieve the number. |
| **7. External Validity** | Does the test distribution match the target workload's messiness, scale, and constraints? |

---

## 4. Ambition in Range: Borrow Methods, Never Roleplay

Complex problems rarely respect academic department boundaries. You can bring 5 fields to bear on a problem for pennies of compute—**provided you borrow their operational methods rather than engaging in theatrical persona roleplay.**

### Step 1: Replace Nouns with Verbs
Strip the conventional noun of the deliverable to reveal the underlying functional problem:
- *"Write a competitor analysis doc"* $\rightarrow$ *"Identify where incumbents are structurally locked in by their unit economics or architecture, and prove which wedge wins."*
- *"Create an incident postmortem"* $\rightarrow$ *"Trace the exact feedback loop that amplified a small perturbation into an outage and prove our fix dampens it."*
- *"Summarize user research"* $\rightarrow$ *"Separate stated preferences from revealed behavioral bottlenecks in the event logs."*

### Step 2: Apply Cross-Disciplinary Method Lenses

Instead of asking *"What would a [persona] say?"*, ask **"What verification procedure does a top [discipline] execute?"**

| Discipline | Methodological Lens to Borrow (No Roleplay) |
| :--- | :--- |
| **Forensic Accountant / Short Seller** | Reconcile totals against raw line items; check footnotes and excluded categories; hunt for survivorship bias, denominator manipulation, and unrecorded liabilities/costs. |
| **Epidemiologist / Biostatistician** | Audit for censoring, selection bias, immortal-time bias, and confounders; use survival curves, hazard ratios, and intention-to-treat vs. per-protocol splits. |
| **Control & Reliability Engineer** | Map feedback loops, gain, dead-time delays, queue saturation (Little's Law, Kingman's formula), cascading failure modes, and observability blind spots. |
| **Experimental Physicist** | Check dimensional consistency, conservation laws (mass/energy/bytes/dollars/requests in = out + stored), order-of-magnitude Fermi bounds, and instrument calibration noise floors. |
| **Investigative Journalist / Historian** | Separate primary contemporaneous records from retrospective rationalizations; require independent corroboration from sources with opposing incentives. |
| **Economist / Mechanism Designer** | Analyze incentive compatibility, Goodhart's Law under optimization pressure, adverse selection, and marginal cost vs. marginal value curves. |

---

## 5. Compute-Scaled Multi-Agent Research (Without Context Pollution)

When a research question spans many sources, large logs, or ambiguous competing explanations, spend inference compute structurally rather than stuffing everything into one context window:

1. **Context Isolation (High-Noise Substrate $\rightarrow$ Compact Evidence Table):**
   Delegate noisy reading (scanning 30 files, parsing huge logs, reading long papers) to an isolated worker/subagent with a strict extraction schema. Have it return **exact citations, file/line links, raw numbers, and reproducible commands**—keeping the lead research context clean for synthesis and crux design.
2. **Nominal Group Technique (NGT) for Competing Hypotheses:**
   When investigating an ambiguous root cause or architectural tradeoff, launch 2+ independent agents (ideally across distinct model families/providers) to investigate competing hypotheses **in isolation**. Do not let them read each other's intermediate reasoning before committing to an evidence-backed finding—early cross-talk triggers sycophantic consensus collapse.
3. **Blind Adversarial Verification (The Outside Judge Agent):**
   Hand your final claim, dataset, and reproduction script—*without your persuasive narrative*—to a fresh verifier agent whose sole instruction is to falsify the claim, find a confounder, or break the reproduction script.
4. **Durable Negative Memory (`tried_and_failed`):**
   Always record ruled-out hypotheses, dead-end queries, and failed probes explicitly so follow-up turns or collaborating agents never waste compute re-testing falsified paths.
