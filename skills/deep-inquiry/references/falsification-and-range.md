# Strong Inference, Falsification, Source Tiers & Cross-Disciplinary Range

Use this playbook to prevent confirmation bias, single-origin citation echoes, paper-shaped misinformation poisoning, and premature stopping.

---

## 1. Pre-Registering Priors, Sub-Questions & Sufficiency Conditions

Enterprise deep-research studies (*Don't Stop Early*, `arXiv:2604.24978`) show that naive agent loops fail via uneven coverage, context bloat, and quitting at the first plausible paragraph. Before running your first search or query, write down a compact research plan:

| Sub-Question | Starting Prior & Confidence | Competing Hypotheses ($H_1, H_2, H_{\text{null}}$) | Sufficiency Condition (What Settles It) |
| :--- | :--- | :--- | :--- |
| *e.g., Does library X handle 10k msg/s under 10ms p99?* | *Likely yes (~65%), based on README claims* | $H_1$: Meets target; $H_2$: GC pauses spike p99 > 50ms; $H_{\text{null}}$: Benchmark workload doesn't match ours | *Tier 1 local benchmark script run across 100k messages with our payload shape* |
| *e.g., Why did retention drop in Cohort B?* | *Onboarding friction (~50%)* | $H_1$: Onboarding step 3 dropoff; $H_2$: Acquisition channel mix shift; $H_{\text{null}}$: Right-censoring artifact | *Kaplan-Meier survival curve stratified by channel + step completion on raw event logs* |

**The Two-Strike Rule:**
- Do not quit just because a problem looks hard—switch source tiers, switch instruments, or borrow another discipline's method (`PaperBench`).
- Do not grind endlessly on a dead end—after **two failed attempts** with the same query pattern or approach, change the approach or record the exact access gap in `tried_and_failed`.

---

## 2. The 4-Tier Source Ladder & Provenance Tracking

Because deep-research agents are highly vulnerable to "paper-shaped" misinformation regardless of search rank (*Is Deep Research Reliable?*, `arXiv:2607.20891`), enforce strict source climbing and provenance tracking as claims enter your notes:

1. **Tier 1 — The Thing Itself (Highest Authority):**
   Raw datasets, source code, live APIs, event/crash logs, git blame/bisect history, regulatory filings, or executing the software/benchmark yourself.
2. **Tier 2 — Primary Documents:**
   The paper's methods, tables, and appendix (never just the abstract), official protocol specifications, changelogs, and raw benchmark results files.
3. **Tier 3 — Expert Secondary:**
   Technical write-ups, postmortems, and replication reviews by maintainers or domain practitioners.
4. **Tier 4 — Discovery Only (Never Evidence):**
   Aggregators, news articles, SEO summaries, social threads, and forums. Use Tier 4 strictly to locate Tiers 1–3.

### Anti-Echo Provenance Checklist
For every load-bearing claim, verify before citing:
- **Origin Trace:** Who actually measured this number? If three blogs and a survey paper all cite the same vendor table, you have **one source**, not four.
- **Late-Arrival Skepticism:** In `arXiv:2607.20891`, misleading documents injected right before synthesis induced an ~85% false-conclusion rate. Treat any late-arriving claim that flips your conclusion as `[Unverified]` until corroborated by Tier 1 execution or independent Tier 2 data.

---

## 3. John Platt's Strong Inference & Bidirectional Search

In 1964, physicist John R. Platt observed that fields practicing **Strong Inference** progress orders of magnitude faster than fields practicing narrative description:

1. **Formulate Multiple Competing Hypotheses ($H_1, H_2, \dots, H_{\text{null}}$).**
2. **Devise the Crucial Experiment (Double-Crux):** State up front what observation falsifies $H_1$ and what falsifies $H_2$. If every outcome is compatible with your narrative, you are collecting illustrations, not doing research.
3. **Execute the Probe Cleanly.**
4. **Recycle:** Log falsified paths in `tried_and_failed` and refine surviving hypotheses.

### Constructive vs. Adversarial Search Templates
Pair every positive search with an explicit **Disconfirmation Search**:

| Constructive Search (Upper Bound) | Adversarial / Disconfirmation Search (Short-Seller Audit) |
| :--- | :--- |
| `[task / problem] state of the art benchmark [year]` | `[method / paper] replication failure critique limitations` |
| `[system] technical report architecture implementation` | `[benchmark / metric] gaming contamination Goodhart flaws` |
| `[phenomenon] causal mechanism empirical dataset` | `[technology / library] production postmortem bottleneck scale limits` |
| `[problem] exact formulation solver algorithm` | `[X] vs [Y] independent benchmark apples-to-apples baseline` |

---

## 4. Comparable Evidence Extraction Schema (7 Columns)

Never compare two papers, tools, or cohorts using headline numbers alone. Normalize across these seven dimensions:

| Dimension | What to Audit Before Comparing |
| :--- | :--- |
| **1. Primary Artifact** | Did we inspect the Tier 1/2 code, raw data, or methods table, or only an abstract/blog? |
| **2. Baseline Parity** | Was the baseline given the same compute, hyperparameter tuning, and harness effort as the proposed method? |
| **3. Sample & Distribution** | Sample size ($N$), dataset split, tail difficulty, and whether easy/contaminated items dominate the average. |
| **4. Metric & Aggregation** | Mean vs. median/`p99`, `pass@1` vs. `pass@k`, absolute vs. relative lift (watch for huge relative % on tiny base rates). |
| **5. Variance & Uncertainty** | Confidence intervals, standard error across seeds/runs, and multiple-testing correction. |
| **6. Resource / Unit Economics** | Wall-clock latency, memory footprint, token/compute cost, and operational complexity. |
| **7. External Validity** | Does the test distribution match the target workload's messiness, scale, and constraints? |

---

## 5. Ambition in Range: Borrow Methods, Never Roleplay

Restate the deliverable by replacing **nouns with verbs** (*not "a market report," but "convincing a skeptical buyer that demand is real and growing"*), then borrow the **verification methods** of fields built for those verbs—never theatrical persona roleplay:

| Discipline | Methodological Lens to Execute (Zero Roleplay) |
| :--- | :--- |
| **Short Seller / Red Team** | Hunt for the single load-bearing assumption, omitted baseline, or incentive distortion that breaks the thesis. |
| **Forensic Accountant** | Reconcile totals against raw line items across sources; explain every discrepancy and footnote exclusion. |
| **Replication Scientist** | Attempt to reproduce the headline result from raw artifacts; catalog unstated dependencies and fragile seeds. |
| **Epidemiologist / Biostatistician** | Audit for survivorship bias, right-censoring, immortal-time bias, and confounders; use survival curves and hazard ratios. |
| **Control & Reliability Engineer** | Map feedback loops, gain, dead-time delays, queue saturation (Little's Law, Kingman's formula), and cascading failures. |
| **Experimental Physicist** | Check dimensional consistency, conservation laws (bytes/requests/dollars in = out + stored), and Fermi bounds. |
| **Investigative Journalist** | Find who has first-hand exposure and compare contemporaneous primary records against retrospective PR. |

---

## 6. Compute-Scaled Multi-Agent Research & Outside Judges

1. **Context Isolation (High-Noise Substrate $\rightarrow$ Compact Evidence Table):**
   When subagents or worker threads are available, fan out independent angles or noisy reading (20+ files, large logs, papers) with explicit boundaries, sufficiency conditions, and a structured output format.
2. **Nominal Group Technique (NGT) for Competing Hypotheses:**
   Have 2+ independent agents investigate competing hypotheses in isolated contexts before comparing evidence—preventing early cross-talk and sycophantic convergence.
3. **The Independent Verifier (Outside Judge):**
   Keep a separate verifier agent (or deterministic script) that did none of the original research. Hand it only the claims, sources, and reproduction scripts, and instruct it to refute them.

---

## 7. Primary Sources for the Empirical Anchors

1. **METR Frontier Time Horizons & Risk Reports:** `https://metr.org/blog/2026-05-19-frontier-risk-report/` & `https://metr.org/time-horizons`
2. **Tool-Heavy Agent Exoplanet Discovery in TESS Data (Oct 2026):** `https://cybernews.com/tech/claude-code-possible-exoplanet-found-in-nasa-data/` & `https://gizmodo.com/did-claude-help-an-amateur-astronomer-discover-a-new-planet-2000824393`
3. **PaperBench & Replication Persistence:** `https://arxiv.org/abs/2504.01848` (`PaperBench`) & `https://github.com/jjakimoto/research-issues/issues/1608` (`ReplicationBench`)
4. **Credulity & Paper-Shaped Misinformation in Deep Research (2026):** *Is Deep Research Reliable? Misleading Knowledge Induces False Conclusions*, `https://arxiv.org/abs/2607.20891`
5. **Evidence-Aware Termination & Sufficiency Conditions (2026):** *Don't Stop Early: Enterprise Deep Research with Evidence-Aware Termination*, `https://arxiv.org/abs/2604.24978`
6. **Jagged Frontier & Survivorship Bias (Oct 2026):** Terence Tao, *"Math 2.0"*, `https://terrytao.wordpress.com/2026/10/10/math-2-0/`
7. **Multi-Agent Research Architecture:** Anthropic Engineering, *"How we built our multi-agent research system"*, `https://www.anthropic.com/engineering/multi-agent-research-system`
8. **Three-Dimensional Ambition (Altitude, Depth, Range):** Felix Rieseberg, *"How to be more ambitious: A tutorial for humans with models"*, `https://felixrieseberg.com/how-to-be-more-ambitious-a-tutorial-for-humans-with-models/`
