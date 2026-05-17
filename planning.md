# Research Plan: LLM and Loopholes

## Motivation & Novelty Assessment

### Why This Research Matters
LLMs are often deployed in settings where an incorrect but confident answer is materially worse than an explicit abstention. If models exploit the implicit "say something" loophole when they are uncertain or when a request is impossible to satisfy, that creates concrete risks for search, education, research assistance, and agentic workflows.

### Gap in Existing Work
The literature in `literature_review.md` shows strong coverage of individual failure modes such as hallucination, truthfulness errors, and abstention failure, but there is little unified empirical work testing whether these are connected by a common answer-anyway pressure dynamic. Public benchmarks typically measure one failure mode at a time rather than the tradeoff between abstention, fabricated compliance, and weak pseudo-compliance across prompt conditions.

### Our Novel Contribution
This project operationalizes "loophole use" as a model choosing to provide a low-quality or fabricated answer instead of cleanly abstaining when the task is impossible, underspecified, or knowledge-intensive. The novelty is a cross-benchmark design that manipulates answer pressure while holding question sets fixed, then measures how often real API models switch from abstention to incorrect or fabricated output.

### Experiment Justification
- Experiment 1: `SimpleQA` tests whether answer pressure turns uncertainty into more incorrect attempted answers on short factual questions.
- Experiment 2: `TruthfulQA` tests whether answer pressure increases plausible-sounding falsehoods on misconception-heavy questions.
- Experiment 3: `HALoGEN` false-presupposition prompts test whether models exploit impossible list requests by fabricating compliant-looking outputs instead of abstaining.

## Research Question
Do LLMs increase fabricated, incorrect, or pseudo-compliant answers when a prompt pressures them to answer rather than abstain, especially on questions they are likely not to know or requests that are impossible to satisfy?

## Background and Motivation
Prior work suggests the relevant behaviors are distributed across several benchmark traditions. `SimpleQA` distinguishes correct, incorrect, and not-attempted answers; `TruthfulQA` captures misconception-driven false answers; `HALoGEN` includes false-presupposition prompts where a correct system should refuse or abstain. Inspired by the user hypothesis, this study treats those behaviors as related manifestations of a loophole: satisfying the surface demand to "answer" without satisfying the underlying epistemic demand to be correct or honest about uncertainty.

## Hypothesis Decomposition
- H1: On factual QA, a forced-answer prompt will reduce abstention and increase incorrect attempts relative to an abstention-friendly prompt.
- H2: On misconception-heavy QA, answer pressure will increase incorrect-but-confident responses more than it increases correct responses.
- H3: On impossible false-presupposition prompts, removing the abstention escape hatch will sharply increase fabricated list outputs.
- H4: Stronger models may still exhibit the pattern, but with smaller effect sizes than weaker or smaller frontier variants.

Independent variables:
- Model: `gpt-4.1`, `gpt-5-mini`
- Prompt condition:
  - `baseline`
  - `abstain_allowed`
  - `forced_answer`
- Benchmark/task:
  - `SimpleQA`
  - `TruthfulQA`
  - `HALoGEN_false_presupposition`

Dependent variables:
- Correct rate
- Incorrect rate
- Not-attempted / abstention rate
- Bluff rate: incorrect attempted answers among all examples
- Fabrication rate on impossible list prompts
- Accuracy conditional on attempting an answer

Alternative explanations to monitor:
- Prompt-format sensitivity rather than epistemic behavior
- Judge model bias in grading free-form answers
- Dataset slice difficulty imbalance

## Proposed Methodology

### Approach
Run real-model API evaluations on three benchmark slices using controlled prompt variants that change the incentives around abstention. Use benchmark-native gold answers where possible, reuse SimpleQA-style LLM grading for free-form correctness, and build an exact parser/evaluator for `HALoGEN` false-presupposition prompts.

### Experimental Steps
1. Load benchmark subsets from local `datasets/` and stratify deterministic samples with a fixed seed.
2. Define prompt variants that preserve task content while varying pressure to answer or abstain.
3. Query `gpt-4.1` and `gpt-5-mini` with temperature `0`.
4. Grade `SimpleQA` and `TruthfulQA` outputs as `CORRECT`, `INCORRECT`, or `NOT_ATTEMPTED` using a real LLM judge and benchmark answer sets.
5. Grade `HALoGEN` false-presupposition outputs with rule-based checks against the known valid item sets and the explicit abstention token.
6. Compute descriptive statistics, pairwise condition comparisons, confidence intervals, and effect sizes.
7. Inspect failure cases to distinguish honest abstention from pseudo-compliance or fabricated compliance.

### Baselines
- `baseline`: answer concisely with no extra uncertainty instruction
- `abstain_allowed`: explicitly instruct the model to say `I don't know` or equivalent if uncertain
- `forced_answer`: explicitly prohibit abstention and require a best-effort answer

### Evaluation Metrics
- `attempt_rate`
- `correct_rate`
- `incorrect_rate`
- `abstain_rate`
- `accuracy_given_attempt`
- `bluff_rate`
- `halogen_valid_list_rate`
- `halogen_fabrication_rate`

These metrics separate safe non-attempts from harmful attempted answers and directly quantify the user’s "say something anyway" hypothesis.

### Statistical Analysis Plan
- Primary comparison: paired bootstrap confidence intervals over per-example outcome differences between prompt conditions.
- Secondary tests:
  - McNemar tests for paired binary outcomes such as `attempted` vs `not attempted`
  - Wilcoxon signed-rank tests on per-example binary differences where appropriate
- Significance level: `alpha = 0.05`
- Multiple-comparison control: Benjamini-Hochberg across the main condition contrasts within each benchmark
- Effect sizes:
  - Risk difference for binary outcome rates
  - Cohen's h for changes in proportions

## Expected Outcomes
Support for the hypothesis would look like a consistent shift from abstention to incorrect or fabricated answers under `forced_answer`, especially on `HALoGEN` impossible prompts and harder factual questions. Refutation would look like models maintaining correctness or honest abstention even when pressured to answer.

## Timeline and Milestones
1. Resource review and planning: complete first
2. Environment and dependency verification: immediate next step
3. Experiment script implementation: one script for data loading, API calling, grading, and analysis
4. Benchmark runs and cached result collection
5. Statistical analysis and visualization
6. Final documentation in `REPORT.md` and `README.md`

## Potential Challenges
- API grading can be noisy
- Frontier model availability or naming can differ across accounts
- Some free-form answers may be semantically correct but hard to grade automatically
- Large benchmark slices could make execution slow or expensive

Mitigations:
- Use deterministic seeds and temperature `0`
- Cache all raw responses and grades
- Start with moderate benchmark slices
- Include a small manual error analysis sample in the report

## Success Criteria
- All three experiments run on real API models with saved raw outputs
- `REPORT.md` contains actual quantitative results and representative examples
- The analysis directly answers whether answer pressure increases loophole-like behavior
- The code is reproducible from the workspace with the isolated `.venv`
