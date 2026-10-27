# Depth, Altitude & Field-Leading Instruments Playbook

Use this playbook to upgrade shallow research prompts into high-altitude, deep-substrate empirical investigations. When prompted to "research like an expert," never merely adopt expert *vocabulary*—switch to the actual **raw substrates, statistical/computational instruments, and external verification judges** used by top practitioners.

---

## 1. The Four-Question Depth Upgrade

Before executing any substantive research or analysis task, run this transformation (adapted from Felix Rieseberg):

> *I want a **deeper** version of this task, not a bigger one:*
> 1. **Expert Delta:** What would a top professional in this field do here that the prompt didn't ask for?
> 2. **Rawest Substrate:** What is the rawest material they would start from instead of what has already been digested?
> 3. **Specific Instruments:** What exact statistical models, databases, solvers, or diagnostic tools would they run?
> 4. **Outside Judge:** What external signal—other than the model's or user's opinion—would prove the result is right?

### Concrete Upgrade Examples

| User Prompt (Shallow) | Bulk Response (Anti-Pattern) | Deep Inquiry Upgrade (Altitude + Depth) |
| :--- | :--- | :--- |
| *"Put together a quarterly review of our metrics."* | Fill a template with summary numbers and write 5 pages of generic commentary. | **Altitude + Depth:** Query raw event/revenue tables (`duckdb`), decompose variance by cohort, identify the 3 most urgent decisions with for/against evidence, and **backtest a leading indicator on historical logs** showing it would have caught this quarter's anomalies weeks earlier. |
| *"Why are users churning?"* | Brainstorm 8 plausible UX reasons or summarize feedback tickets in a Markdown table. | **Adversarial Substrate + Prediction:** Test whether folk wisdom (*"churn is an onboarding issue"*) actually reproduces in raw session logs using Kaplan-Meier survival curves and Cox proportional hazards. Then simulate customer trajectories and validate an early-warning churn predictor on held-out cohorts. |
| *"Which database / queue / parser should we use?"* | Summarize Hacker News threads, vendor READMEs, and qualitative pros/cons (`Fast / Medium / Slow`). | **15-Minute Executable Probe:** Write a 40-line benchmark script in `scratch/` replaying the actual payload distribution and concurrency target; measure `p50`/`p99` latency, RSS memory, and failure recovery under fault injection. |
| *"Review these papers on method X."* | Paraphrase each paper's abstract and conclusion into a literature review. | **Comparable Extraction + Audit:** Build a normalized extraction table locking compute budget, dataset split, baseline tuning parity, and error bars. Check whether claimed gains survive when baseline hyperparameters match. |

---

## 2. Instrument Escalation by Domain

When you catch yourself reaching for prose reasoning or hand-typed Markdown tables, switch to the real instrument for the domain:

### A. Data Science, Product Analytics & Statistics
- **Rawest Substrates:** Parquet/CSV exports, SQLite/Postgres dumps, raw JSONL event streams, git commit/PR timestamps, raw experiment assignment logs.
- **Instruments to Run:**
  - **Fast Aggregation:** `duckdb` CLI or Python `polars`/`duckdb` over millions of rows in seconds—never sample 20 rows into the LLM context window and eyeball them.
  - **Distributions & Uncertainty:** Report `p10`/`p50`/`p90`/`p99`, interquartile range (IQR), and **non-parametric bootstrap confidence intervals** (`scipy.stats.bootstrap`) rather than naked means that hide heavy tails or multimodal splits.
  - **Time-to-Event & Retention:** Survival analysis (Kaplan-Meier curves, log-rank tests, Cox hazards) to handle right-censored data properly instead of naive conversion ratios.
  - **Causal & Confounder Checks:** Stratification (Simpson's paradox audit), difference-in-differences, propensity weighting, or regression controlling for cohort/seasonality (`statsmodels`).
- **Outside Judge:** Out-of-time / held-out split accuracy, calibration curve (Brier score / log-loss), and permutation placebos (shuffling labels to confirm the pipeline doesn't hallucinate signal).

### B. Systems, Performance & Codebase Forensics
- **Rawest Substrates:** Source AST/call graphs, `git log -S` / `git bisect` history, flamegraphs, syscall/network captures, core dumps, query execution plans (`EXPLAIN ANALYZE`).
- **Instruments to Run:**
  - **Search & Structure:** `rg` (ripgrep), `git log -L` (line-level evolution), symbol/reference graphs.
  - **Timing & Profiling:** `hyperfine`, `python3 -m timeit`, `cProfile` / `py-spy`, `perf`, memory allocators (`tracemalloc`), SQL `EXPLAIN ANALYZE`.
  - **Correctness & Edge Cases:** Property-based testing (`hypothesis` / `fast-check`), deterministic state-machine fuzzing, or SMT/constraint solving (`z3`) for scheduling/routing/permission invariants.
- **Outside Judge:** A minimal failing reproduction script that fails before the hypothesized cause is controlled and passes deterministically after, plus latency/throughput distributions across repeated runs.

### C. Empirical ML, Evals & AI Systems Research
- **Rawest Substrates:** Raw evaluation transcripts/trajectories (`.jsonl`), per-task pass/fail matrices, grader source code, token/cost logs, raw prompt/tool payloads.
- **Instruments to Run:**
  - **Paired Comparisons:** McNemar's test or paired bootstrap over the exact same task IDs—never compare aggregate percentages across different task subsets or harnesses without checking task-level overlap.
  - **Reliability vs. Discovery:** Measure both `pass@1` / `pass^k` (unattended reliability) and `pass@k` (verifier-selected upper bound).
  - **Transcript Forensics:** Programmatically classify failure modes across all trajectories (environment error vs. grader bug vs. reward hacking vs. context truncation vs. reasoning failure).
- **Outside Judge:** Held-out contamination-free task set, deterministic executable verifier, and blinded human/cross-provider audit of grader false positives.

---

## 3. Generative Knowledge & Counterfactual Backtesting

Descriptive research tells the user what already happened. Deep inquiry produces **new predictive knowledge**:

1. **Reproduce Reality in a Model/Simulation:**
   Write a lightweight mathematical model, state machine, or Monte Carlo simulation calibrated to the raw historical logs. Verify first that it reproduces the known historical distributions.
2. **Search for Unnoticed Leading Signals:**
   Query the raw features/events preceding historical failures, churn, or regime shifts. Rank candidate signals by information gain / hazard ratio while penalizing multiple-hypothesis dredging (Bonferroni / Benjamini-Hochberg false-discovery control or train/test split).
3. **Validate on Unseen Data (The Out-of-Sample Gate):**
   Fit the signal strictly on $t < T_{\text{split}}$ and evaluate its precision/recall and lead time on $t \ge T_{\text{split}}$.
4. **Run the Altitude Backtest:**
   When recommending a new policy, alert, or workflow, answer: *"If we had run this exact rule over the last 6 months of raw history, which exact incidents would it have caught early, how many false alarms would it have fired, and what would it have cost?"*

---

## 4. Calibrating Ambition (The 200ms & Dantzig Principle)

Models and humans chronically self-censor research scope because a goal sounds "too hard" or "unreasonable."
- **Refuse premature qualitative fallback:** If asked a quantitative question without clean data, do not immediately retreat to vague prose. Construct a **Fermi bound** from independent measurable proxies, pull public/local datasets, or build a synthetic stress-test that bounds the answer within an order of magnitude.
- **Test extreme targets:** Asking *"how do we make this 10% better?"* invites incremental patches; asking *"what physical or algorithmic constraint stops this from being 20× faster or 10× cheaper?"* forces you to identify the true bottleneck (I/O bound, serialization overhead, sequential round-trips) from first principles.
