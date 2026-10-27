# deep-inquiry

An agent skill that pushes research and technical investigation past **search-and-summarize**: recalibrating stale priors, climbing to raw data and primary sources, running code and statistical/computational instruments instead of quoting, maintaining competing hypotheses (**Strong Inference**), verifying claims as they enter notes, enforcing an **outside judge**, and stopping on pre-registered sufficiency evidence rather than the first plausible paragraph.

Built as the research counterpart to [`bitter-lesson`](https://github.com/3xC1ibR/bitter-lesson).

## Why This Exists (Dated Anchors — October 2026)

Default agent research—search, skim snippets, summarize the first plausible sources, stop—fails in two directions at once:

1. **Not ambitious enough (Reading Instead of Doing):** It treats research as reading about things when the agent has a full computer to pull the raw dataset, read the implementation, query `duckdb`, fit survival curves, run benchmarks, or build simulations. And it anchors on training-time capability priors, proposing as "stretch goals" things that have been routine for months.
2. **Not skeptical enough (Credulity & Echo Laundering):** It searches for confirmation, counts three blogs quoting one press release as three independent sources, falls for paper-shaped misinformation (`arXiv:2607.20891` showed a single misleading paper-formatted doc jumped false conclusions from **0% to ~55–85%**), quits early on hard steps (`PaperBench` showed preventing early stopping nearly doubled `o1` replication scores from **13.2% $\rightarrow$ 24.4%**), and grades its own work.

## What the Skill Enforces

- **[`skills/deep-inquiry/SKILL.md`](skills/deep-inquiry/SKILL.md)** — The 9-step Deep Inquiry loop:
  1. **Find the Question Behind the Question (Altitude):** Identify the decision at stake and what happens *after* the answer (often a prototype, benchmark harness, or backtested monitor beats a static report).
  2. **Write Down Priors, Competing Hypotheses & the Expert Bar:** Record starting belief/confidence, formulate competing hypotheses ($H_1, H_2, H_{\text{null}}$ + double-crux), pre-register per-sub-question **sufficiency conditions** (`arXiv:2604.24978`), and run the **4-question Depth upgrade** (*What would a top expert do? What is the rawest substrate? What exact instruments do they use? What outside judge proves it right?*).
  3. **Treat Anything About "Now" as Unknown Until Checked:** Search live (last 6–12 months) before calling anything state-of-the-art, impossible, an open problem, or an ambitious stretch goal.
  4. **Climb to the Rawest Material You Can Reach:** Enforce a 4-tier source ladder (Tier 1: the dataset/code/logs/API itself $\rightarrow$ Tier 2: primary paper methods/specs $\rightarrow$ Tier 3: maintainer write-ups $\rightarrow$ Tier 4: news/SEO/forums for discovery only, never evidence).
  5. **Use the Instruments, Not Just the Vocabulary:** Replace qualitative prose and hand-typed Markdown tables with `duckdb`/`polars`, bootstrap CIs, Kaplan-Meier/Cox survival analysis, `hyperfine` micro-benchmarks, AST queries, `z3`, and Monte Carlo simulations.
  6. **Borrow Other Fields' Methods (Range Without Roleplay):** Replace nouns with verbs and execute the verification procedures of short sellers, forensic accountants, replication scientists, epidemiologists, physicists, and investigative journalists—without persona roleplay.
  7. **Verify Claims as They Arrive:** Track provenance, upstream independence (anti-echo check), and status tags (`[Verified: ran/primary]`, `[Supported: independent secondary]`, `[Unverified / single-source]`), plus mandatory disconfirmation searches.
  8. **Get an Outside Judge:** Validate via executable ground truth or an epistemically independent refutation agent—never self-grade.
  9. **Stop on Sufficiency Evidence, Not Fatigue or Plausibility:** Apply the Two-Strike Rule (switch source tiers/instruments/methods rather than quitting early or grinding on the same query).
- **[`skills/deep-inquiry/references/depth-and-instruments.md`](skills/deep-inquiry/references/depth-and-instruments.md)** — Concrete 4-question Depth upgrades, domain-by-domain instrument escalation tables (Data Science/Stats, Systems/Codebase Forensics, Empirical ML/Evals), generative simulation, and historical backtesting.
- **[`skills/deep-inquiry/references/falsification-and-range.md`](skills/deep-inquiry/references/falsification-and-range.md)** — Sufficiency-condition templates, the 4-tier source ladder, John Platt's Strong Inference protocol, the 7-column Comparable Evidence Extraction Schema, cross-disciplinary method lenses, compute-scaled multi-agent NGT research, and primary sources.

## Installation

```bash
git clone https://github.com/3xC1ibR/deep-inquiry.git
ln -sfn "$(pwd)/deep-inquiry/skills/deep-inquiry" ~/.agents/skills/deep-inquiry
```

## License

MIT
