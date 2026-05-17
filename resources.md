# Resources Catalog

## Summary

This document catalogs the papers, datasets, and code repositories gathered for the research project "LLM and Loopholes".

## Papers

Total papers downloaded: 7

| Title | Authors | Year | File | Key Info |
|------|---------|------|------|---------|
| Sleeper Agents: Training Deceptive LLMs that Persist Through Safety Training | Hubinger et al. | 2024 | `papers/2401.05566_sleeper_agents.pdf` | Deceptive backdoors persist through safety training |
| TruthfulQA: Measuring How Models Mimic Human Falsehoods | Lin, Hilton, Evans | 2021 | `papers/2109.07958_truthfulqa.pdf` | Foundational falsehood benchmark |
| HaluEval | Li et al. | 2023 | `papers/2305.11747_halueval.pdf` | 35K hallucination benchmark |
| RefChecker | Hu et al. | 2024 | `papers/2405.14486_refchecker.pdf` | Claim-triplet hallucination checker |
| Measuring short-form factuality in large language models | Wei et al. | 2024 | `papers/2411.04368_simpleqa.pdf` | Best direct benchmark for "know when you don't know" |
| HALoGEN | Ravichander et al. | 2025 | `papers/2501.08292_halogen.pdf` | Multi-domain hallucination benchmark with verifiers |
| AbstentionBench | Kirichenko et al. | 2025 | `papers/2506.09038_abstentionbench.pdf` | Benchmark for abstention on unanswerable questions |

See `papers/README.md` for details.

## Datasets

Total datasets downloaded/materialized: 5

| Name | Source | Size | Task | Location | Notes |
|------|--------|------|------|----------|-------|
| HaluEval | RUCAIBox repo | 34,507 records | Hallucination recognition | `datasets/halueval/` | Fully materialized locally |
| HALoGEN | Upstream repo | ~65 MB | Multi-domain hallucination analysis | `datasets/halogen/` | Includes prompts and hallucination CSVs |
| TruthfulQA | Upstream repo | 790 rows | Truthfulness | `datasets/truthfulqa/` | Current maintained CSV, not original 817-row release |
| SimpleQA | OpenAI public CSV | 4,326 rows | Short-form factuality and abstention | `datasets/simpleqa/` | Fully materialized locally |
| AbstentionBench support files | facebookresearch repo | small metadata bundle | Abstention benchmark setup | `datasets/abstentionbench/` | Partial local materialization only |

See `datasets/README.md` for loading and download instructions.

## Code Repositories

Total repositories cloned: 6

| Name | URL | Purpose | Location | Notes |
|------|-----|---------|----------|-------|
| RefChecker | github.com/amazon-science/RefChecker | Fine-grained hallucination checking | `code/refchecker/` | Benchmark data requires separate download script |
| HaluEval | github.com/RUCAIBox/HaluEval | Hallucination benchmark | `code/halueval/` | Ships with usable local data |
| HALoGEN | github.com/AbhilashaRavichander/HALoGEN | Multi-domain hallucination eval | `code/halogen/` | Includes prompts, outputs, verifiers |
| AbstentionBench | github.com/facebookresearch/AbstentionBench | Abstention evaluation | `code/abstentionbench/` | Best benchmark for uncertainty abstention |
| simple-evals | github.com/openai/simple-evals | SimpleQA reference harness | `code/simple-evals/` | Contains SimpleQA evaluation logic |
| TruthfulQA | github.com/sylinrl/truthfulqa | Truthfulness benchmark | `code/truthfulqa/` | Includes benchmark CSV and eval code |

See `code/README.md` for details.

## Resource Gathering Notes

### Search Strategy

The search focused on four subthemes:
- deliberate or strategic deception
- hallucination and fabrication
- truthfulness versus misconception imitation
- abstention when a question should not be answered definitively

The initial plan was to use the local `paper-finder` helper. On May 17, 2026, both `fast` and `diligent` calls stalled without returning practical results, so manual collection from arXiv, GitHub, and linked project materials was used instead.

### Selection Criteria

- Strong match to the research hypothesis
- Publicly accessible paper
- Benchmark data and/or code available
- Direct usefulness for an experiment runner

### Challenges Encountered

- `paper-finder` did not return on time
- The current Hugging Face `datasets` stack no longer supports some legacy script-based dataset loaders, which blocked automatic materialization of full `AbstentionBench`
- RefChecker's benchmark release path is less turnkey than its checker framework

### Gaps and Workarounds

- No single public benchmark directly captures all "loophole" behavior
- Workaround: combine deception, truthfulness, hallucination, and abstention benchmarks
- `AbstentionBench` was documented and partially materialized through repo assets even though the full dataset bundle was not pulled locally

## Recommendations for Experiment Design

1. **Primary dataset(s)**: Start with `SimpleQA`, `TruthfulQA`, and `HaluEval`; add `HALoGEN` for broader domain stress tests.
2. **Baseline methods**: Compare raw answer generation, abstention-encouraging prompting, and post-hoc hallucination checking with `RefChecker`.
3. **Evaluation metrics**: Track `correct`, `incorrect`, `not attempted`, hallucination rate, abstention rate, and claim-level contradiction rate.
4. **Code to adapt/reuse**: Reuse `code/simple-evals/simpleqa_eval.py`, `code/truthfulqa/`, `code/halueval/evaluation/`, and `code/refchecker/`.
