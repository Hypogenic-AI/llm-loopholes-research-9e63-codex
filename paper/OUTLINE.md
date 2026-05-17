## Title

Answer Anyway: Prompt Pressure Elicits Fabricated Compliance in Large Language Models

## Abstract

- Problem: LLMs often face pressure to answer even when uncertain or when a request is impossible.
- Gap: Prior work studies deception, hallucination, truthfulness, and abstention separately.
- Approach: Cross-benchmark evaluation on SimpleQA, TruthfulQA, and HALoGEN false-presupposition prompts with three prompt conditions.
- Key evidence: 960 generations from `gpt-4.1` and `gpt-5-mini`; strongest effect on impossible prompts where forced answering produced 100% loophole-attempt rates for both models.
- Significance: Surface-level compliance can displace epistemic honesty, especially on structurally impossible requests.

## Introduction

- Hook: In deployed systems, a confident wrong answer can be worse than a refusal.
- Importance: Answer pressure appears in assistants, search, education, and agent pipelines.
- Gap: Existing benchmarks isolate hallucination, truthfulness, abstention, or deception rather than the answer-pressure tradeoff across them.
- Approach: Hold questions fixed, vary prompt pressure (`baseline`, `abstain_allowed`, `forced_answer`), and measure shifts from abstention to attempted answers.
- Quantitative preview:
  - HALoGEN impossible prompts: loophole attempt rises from 28.3% to 100% for `gpt-4.1`, and from 31.7% to 100% for `gpt-5-mini`.
  - SimpleQA: `gpt-5-mini` attempt rate rises from 8% to 100% under forced answering, with incorrect rate rising by 82 points.
- Contributions:
  - We define loophole use operationally as attempted compliance when abstention is epistemically correct.
  - We conduct a controlled cross-benchmark study across factual uncertainty and impossible requests.
  - We show the effect is strongest on impossible structured prompts and strongly model-dependent on factual QA.
  - We connect abstention failure to broader answer-pressure dynamics.

## Related Work

- Theme 1: Strategic deception
  - `Sleeper Agents` as evidence of persistent deceptive behavior under training.
  - Position: our work measures observable pseudo-compliance at inference time, not latent backdoors.
- Theme 2: Truthfulness and factuality
  - `TruthfulQA` and `SimpleQA` as benchmarks for plausible falsehoods and calibrated answering.
  - Position: we use both to test whether answer pressure shifts response behavior on fixed question sets.
- Theme 3: Hallucination benchmarks and checkers
  - `HaluEval`, `RefChecker`, and `HALoGEN` provide evaluation traditions for hallucination and verification.
  - Position: we adapt HALoGEN false-presupposition prompts as a clean impossible-request setting.
- Theme 4: Abstention
  - `AbstentionBench` shows abstention remains unsolved.
  - Position: our paper complements it by directly manipulating answer pressure.

## Methodology

- Problem formulation:
  - Independent variables: model, benchmark, prompt condition.
  - Dependent variables: attempted, incorrect, not attempted, accuracy given attempt, loophole attempt, fabricated attempt.
- Experimental setup:
  - Models: `gpt-4.1`, `gpt-5-mini`.
  - Grader: `gpt-4.1-mini` for SimpleQA and TruthfulQA.
  - Temperature 0, seed 42.
- Datasets:
  - 50 SimpleQA, 50 TruthfulQA, 60 impossible + 20 possible HALoGEN prompts.
  - Main loophole analysis uses impossible HALoGEN prompts.
- Evaluation:
  - Categorical grading for factual benchmarks.
  - Rule-based grading for impossible prompts.
- Statistical analysis:
  - Paired risk differences, bootstrap 95% CIs, McNemar tests, BH correction.
- Figure/table plan:
  - Table for HALoGEN impossible prompts.
  - Table for factual benchmarks across SimpleQA and TruthfulQA.
  - Table for primary forced-vs-abstain contrasts.
  - Two figures copied from `figures/`.

## Results

- Main result:
  - Forced answer causes 100% attempted responses on impossible HALoGEN prompts for both models.
  - Fabricated attempt rate reaches 96.7% for `gpt-4.1` and 91.7% for `gpt-5-mini`.
- Factual QA:
  - `gpt-5-mini` shows strong abstention-versus-bluffing tradeoff on both SimpleQA and TruthfulQA.
  - `gpt-4.1` is comparatively insensitive to prompt condition on factual QA.
- Statistical analysis:
  - Report forced-vs-abstain risk differences and FDR-adjusted p-values.
- Failure cases:
  - impossible list fabrication
  - padded or duplicated pseudo-compliance
  - confident factual guessing

## Discussion

- Interpretation:
  - Answer pressure shifts models toward surface compliance.
  - Impossible prompts expose the cleanest loophole behavior.
  - Different models implement abstention policy differently.
- Limitations:
  - Two models, one provider, partial benchmark slices, LLM judge on factual tasks, prompt phrasing sensitivity.
- Broader implications:
  - Systems should not reward “doing something” when abstention is correct.
  - Validators and abstention-friendly policies matter in agent pipelines.

## Conclusion

- Summarize operational definition and cross-benchmark findings.
- Key takeaway: the loophole is real, strongest on structurally impossible prompts, and model-dependent on factual QA.
- Future work: more providers, broader abstention benchmarks, intervention comparison with validators.
