# Downloaded Papers

This directory contains the core papers selected for the topic "LLM and Loopholes".

1. [Sleeper Agents: Training Deceptive LLMs that Persist Through Safety Training](2401.05566_sleeper_agents.pdf)
   - Authors: Evan Hubinger et al.
   - Year: 2024
   - Source: arXiv:2401.05566
   - Why relevant: Directly studies deceptive behavior, trigger-conditioned misbehavior, and failure of standard post-hoc safety training to remove it.
   - Deep reading: Chunked in `papers/pages/sleeper_agents/`.

2. [TruthfulQA: Measuring How Models Mimic Human Falsehoods](2109.07958_truthfulqa.pdf)
   - Authors: Stephanie Lin, Jacob Hilton, Owain Evans
   - Year: 2021
   - Source: arXiv:2109.07958 / ACL 2022
   - Why relevant: Foundational benchmark for false-but-plausible answers when models imitate human misconceptions.

3. [HaluEval: A Large-Scale Hallucination Evaluation Benchmark for Large Language Models](2305.11747_halueval.pdf)
   - Authors: Junyi Li et al.
   - Year: 2023
   - Source: arXiv:2305.11747
   - Why relevant: Large benchmark for hallucination recognition across QA, dialogue, summarization, and general queries.

4. [RefChecker: Reference-based Fine-grained Hallucination Checker and Benchmark for Large Language Models](2405.14486_refchecker.pdf)
   - Authors: Zhengxiang Hu et al.
   - Year: 2024
   - Source: arXiv:2405.14486
   - Why relevant: Fine-grained claim-triplet framework for detecting hallucinations with or without supporting context.
   - Deep reading: Chunked in `papers/pages/refchecker/`.

5. [Measuring short-form factuality in large language models](2411.04368_simpleqa.pdf)
   - Authors: Jason Wei et al.
   - Year: 2024
   - Source: arXiv:2411.04368
   - Why relevant: Measures whether models "know what they know" and whether they appropriately avoid attempting uncertain factual answers.

6. [HALoGEN: Fantastic LLM Hallucinations and Where to Find Them](2501.08292_halogen.pdf)
   - Authors: Abhilasha Ravichander et al.
   - Year: 2025
   - Source: arXiv:2501.08292
   - Why relevant: Broad hallucination benchmark with domain-specific verifiers and released generations from many models.
   - Deep reading: Chunked in `papers/pages/halogen/`.

7. [AbstentionBench: Reasoning LLMs Fail on Unanswerable Questions](2506.09038_abstentionbench.pdf)
   - Authors: Polina Kirichenko et al.
   - Year: 2025
   - Source: arXiv:2506.09038
   - Why relevant: Evaluates selective abstention on unanswerable, underspecified, stale, and subjective questions.
   - Deep reading: Chunked in `papers/pages/abstentionbench/`.

Notes:
- The paper-finder helper was invoked on May 17, 2026 but did not return within practical time bounds in either `fast` or `diligent` mode, so manual retrieval from paper and project sources was used.
- Chunk manifests for the deep-read papers are under `papers/pages/*/*manifest.txt`.
