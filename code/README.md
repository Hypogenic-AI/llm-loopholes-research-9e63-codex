# Cloned Repositories

## Repo 1: RefChecker
- URL: https://github.com/amazon-science/RefChecker
- Purpose: Fine-grained hallucination detection via claim-triplet extraction and checking
- Location: `code/refchecker/`
- Key files: `README.md`, `pyproject.toml`, `benchmark/`, `refchecker/`
- Notes: Strong baseline for post-generation hallucination checking. Benchmark download requires separate script execution under `benchmark/data/download_data.sh`.

## Repo 2: HaluEval
- URL: https://github.com/RUCAIBox/HaluEval
- Purpose: Hallucination benchmark generation, evaluation, and analysis
- Location: `code/halueval/`
- Key files: `README.md`, `data/`, `evaluation/`, `generation/`, `analysis/`
- Notes: Immediately useful because benchmark data ships in-repo. Good for binary hallucination-recognition experiments.

## Repo 3: HALoGEN
- URL: https://github.com/AbhilashaRavichander/HALoGEN
- Purpose: Multi-domain hallucination benchmark with prompts, released generations, verifiers, and scorers
- Location: `code/halogen/`
- Key files: `README.md`, `requirements.txt`, `prompts/`, `model_hallucinations/`, `verifiers/`, `scorers/`
- Notes: High experimental value for studying failure modes across domains. Some verifiers require OpenAI, Together, and Semantic Scholar API access.

## Repo 4: AbstentionBench
- URL: https://github.com/facebookresearch/AbstentionBench
- Purpose: Benchmark for selective abstention on unanswerable or underspecified questions
- Location: `code/abstentionbench/`
- Key files: `README.md`, `main.py`, `configs/dataset/`, `analysis/`, `data/`
- Notes: Upstream README documents 20 datasets and 6 scenarios. Full data retrieval is delegated to the repo workflow.

## Repo 5: simple-evals
- URL: https://github.com/openai/simple-evals
- Purpose: Lightweight eval harness containing SimpleQA reference logic
- Location: `code/simple-evals/`
- Key files: `README.md`, `simpleqa_eval.py`, `simple_evals.py`
- Notes: Useful reference implementation for factuality scoring and non-attempt accounting. The repo is deprecated for new benchmarks but still hosts SimpleQA.

## Repo 6: TruthfulQA
- URL: https://github.com/sylinrl/truthfulqa
- Purpose: Truthfulness benchmark and evaluation scripts
- Location: `code/truthfulqa/`
- Key files: `README.md`, `TruthfulQA.csv`, `truthfulqa/`, `data/`
- Notes: Foundational benchmark for misconception-driven false answers. Includes updated multiple-choice setting and evaluation assets.
