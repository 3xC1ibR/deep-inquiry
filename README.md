# deep-inquiry

An agent skill that upgrades research and technical investigation from **shallow synthesis, vocabulary mimicry, and confirmation bias** to **Strong Inference, raw-substrate forensics, field-leading instruments, and external verification**.

Built as the research counterpart to [`bitter-lesson`](https://github.com/3xC1ibR/bitter-lesson), combining John Platt's **Strong Inference**, Rich Sutton's **Bitter Lesson** (execution & statistical instruments over prose), and Felix Rieseberg's **Altitude / Depth / Range** framework.

## Why This Exists

Left to their default training priors, models fail at research in four predictable ways:

1. **Bulk-Over-Depth RLHF Bias:** Human raters reward long, well-formatted Markdown summaries. When asked to "go deeper," models produce *more words and bullet points* rather than touching raw data or running a decisive test.
2. **Vocabulary-Over-Instrument Mimicry:** When prompted to act like an expert, models switch *vocabulary* without switching *methods*—writing prose arguments or hand-typed Markdown tables when the problem calls for `duckdb`, survival analysis, bootstrap confidence intervals, micro-benchmarks, or formal solvers.
3. **Digested-Source & Confirmation Bias:** Models accept pre-digested summaries, abstracts, and organizational "folk wisdom" at face value, searching only for evidence that confirms the user's premise.
4. **Low Research Self-Efficacy (Premature Surrender):** Models retreat to qualitative hand-waving (*"this would require further study"*) when a 15-minute executable script, simulation, or historical backtest in their shell would answer the question outright.

## What the Skill Enforces

- **[`skills/deep-inquiry/SKILL.md`](skills/deep-inquiry/SKILL.md)** — Core 6-step research workflow:
  1. **Upgrade the Question (Altitude, Depth, Range):** Run the 4-question Depth upgrade (*What would a top professional do? What is the rawest substrate? What exact instruments do they use? What outside judge proves it right?*), look for the goal beyond the goal (Altitude), and replace nouns with verbs to borrow methods across fields (Range).
  2. **Drop to the Rawest Available Substrate:** Bypass pre-digested dashboards, abstracts, and folk wisdom; pull raw logs, primary tables, git history, wire traces, or source code.
  3. **Switch Instruments, Not Vocabulary (The 15-Minute Probe Gate):** Never debate in prose what you can compute in a shell (`duckdb`, `scipy`/`statsmodels`, Kaplan-Meier/Cox survival models, `hyperfine`, AST queries, `z3`).
  4. **Apply Strong Inference & the Bitter Lesson of Research:** Maintain competing hypotheses ($H_1, H_2, H_{\text{null}}$), define the **double-crux** before collecting data, run adversarial/short-seller searches, and favor appreciating artifacts (reproduction scripts, normalized comparison tables, negative-result logs) over depreciating prose.
  5. **Produce New Knowledge & Validate with an Outside Judge:** Move from backward description to generative simulation and **held-out / out-of-sample prediction**; backtest proposed signals against historical incidents; never allow the model to grade itself.
  6. **Classify Evidence Narrowly & Strip Weasel Language:** Tag claims (`[Verified by execution]`, `[Primary empirical source]`, `[Single-source / unaudited]`, `[Hypothesis / unverified prior]`), eliminate lazy phrases (*"studies show..."*), and stop when additional precision no longer changes the decision.
- **[`skills/deep-inquiry/references/depth-and-instruments.md`](skills/deep-inquiry/references/depth-and-instruments.md)** — The 4-question Depth upgrade examples, domain-by-domain instrument escalation (Data Science/Stats, Systems/Codebase Forensics, Empirical ML/Evals), generative simulation, and counterfactual backtesting.
- **[`skills/deep-inquiry/references/falsification-and-range.md`](skills/deep-inquiry/references/falsification-and-range.md)** — John Platt's Strong Inference protocol, bidirectional/adversarial search templates, the 7-column Comparable Evidence Extraction Schema, cross-disciplinary method borrowing without roleplay (Forensic Accountant, Short Seller, Epidemiologist, Control Engineer, Experimental Physicist), and compute-scaled multi-agent NGT research.

## Installation

```bash
git clone https://github.com/3xC1ibR/deep-inquiry.git
ln -sfn "$(pwd)/deep-inquiry/skills/deep-inquiry" ~/.agents/skills/deep-inquiry
```

## License

MIT
