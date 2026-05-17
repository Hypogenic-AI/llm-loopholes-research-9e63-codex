# Downloaded Datasets

This directory contains benchmark data for experiments on deceptive behavior, hallucination, truthfulness, and abstention. Data files are excluded from git by `datasets/.gitignore`.

## Dataset 1: HaluEval

### Overview
- Source: `code/halueval/data/` from `RUCAIBox/HaluEval`
- Size: 34,507 records local
- Format: JSONL
- Task: Hallucination recognition and analysis
- Splits: Benchmark files by task, not train/val/test splits
- License: MIT per upstream repo

### Download Instructions

Local copy already materialized at `datasets/halueval/`.

Recreate from source repo:
```bash
cp -r code/halueval/data datasets/halueval
```

### Loading the Dataset
```python
import json

rows = []
with open("datasets/halueval/qa_data.json") as f:
    for line in f:
        rows.append(json.loads(line))
```

### Sample Data
- Samples saved in `datasets/halueval/samples/`

### Notes
- `general_data.json`: 4,507 human-annotated general-query records
- `qa_data.json`, `dialogue_data.json`, `summarization_data.json`: 10,000 records each
- Seed tasks come from HotpotQA, OpenDialKG, and CNN/DailyMail

## Dataset 2: HALoGEN

### Overview
- Source: `code/halogen/prompts` and `code/halogen/model_hallucinations`
- Size: about 65 MB local
- Format: CSV
- Task: Multi-domain hallucination measurement with verifier outputs
- Splits: Organized by task/domain and model
- License: Check upstream repo for paper/code usage terms

### Download Instructions

Local copy already materialized at `datasets/halogen/`.

Recreate from source repo:
```bash
cp -r code/halogen/prompts datasets/halogen/
cp -r code/halogen/model_hallucinations datasets/halogen/
```

### Loading the Dataset
```python
import pandas as pd

df = pd.read_csv("datasets/halogen/prompts/prompts_biographies.csv")
```

### Sample Data
- Samples saved in `datasets/halogen/samples/`

### Notes
- The paper reports 10,923 prompts across 9 domains; use the paper's count rather than raw CSV row counts when citing the benchmark
- 126 released hallucination-output CSVs from evaluated models
- Useful for domain-by-domain failure analysis rather than a single scalar score

## Dataset 3: TruthfulQA

### Overview
- Source: `sylinrl/truthfulqa` and the benchmark CSV
- Size: 790 questions in current local CSV
- Format: CSV and JSON
- Task: Truthfulness under misleading or misconception-inducing prompts
- Splits: Single benchmark table plus auxiliary evaluation files
- License: Apache 2.0 per upstream repo metadata

### Download Instructions

Local copy already materialized at `datasets/truthfulqa/`.

Recreate from source repo:
```bash
cp code/truthfulqa/TruthfulQA.csv datasets/truthfulqa/
cp code/truthfulqa/TruthfulQA_demo.csv datasets/truthfulqa/
cp -r code/truthfulqa/data datasets/truthfulqa/
```

### Loading the Dataset
```python
import pandas as pd

df = pd.read_csv("datasets/truthfulqa/TruthfulQA.csv")
```

### Sample Data
- Samples saved in `datasets/truthfulqa/samples/`

### Notes
- The current upstream CSV has 790 rows locally, reflecting upstream updates after the original 817-question paper release
- Includes updated binary multiple-choice support and evaluation assets

## Dataset 4: SimpleQA

### Overview
- Source: OpenAI public benchmark CSV
- Size: 4,326 questions
- Format: CSV
- Task: Short-form factuality with explicit `correct` / `incorrect` / `not attempted` grading
- Splits: Single benchmark table
- License: MIT via `openai/simple-evals`

### Download Instructions

Local copy already materialized at `datasets/simpleqa/simple_qa_test_set.csv`.

Direct download:
```bash
curl -L https://openaipublic.blob.core.windows.net/simple-evals/simple_qa_test_set.csv \
  -o datasets/simpleqa/simple_qa_test_set.csv
```

### Loading the Dataset
```python
import pandas as pd

df = pd.read_csv("datasets/simpleqa/simple_qa_test_set.csv")
```

### Sample Data
- Samples saved in `datasets/simpleqa/samples/`

### Notes
- Good fit for testing whether a model abstains instead of bluffing when unsure
- The reference evaluator in `code/simple-evals/simpleqa_eval.py` computes `is_correct`, `is_incorrect`, `is_not_attempted`, `accuracy_given_attempted`, and F1-style summary metrics

## Dataset 5: AbstentionBench Support Files

### Overview
- Source: `facebookresearch/AbstentionBench`
- Size: small local metadata bundle
- Format: JSON and config assets
- Task: Abstention evaluation over 20 datasets
- Splits: Local support files only
- License: Check upstream repo

### Download Instructions

Local support files are at `datasets/abstentionbench/`, copied from the repo.

For the full benchmark, follow the upstream workflow:
```bash
git clone https://github.com/facebookresearch/AbstentionBench.git code/abstentionbench
cd code/abstentionbench
# follow README instructions for automatic dataset retrieval
```

### Loading the Dataset
```python
import json

with open("datasets/abstentionbench/subsampling-indices.json") as f:
    subsampling = json.load(f)
```

### Sample Data
- Local files include subsampling indices and bundled assets only

### Notes
- The upstream README lists 20 constituent datasets across 6 abstention scenarios
- Full automatic materialization was not completed here because the current `datasets` library no longer supports the repo's legacy script-based loader
- This is still enough for the experiment runner to inspect configs and reproduce the official retrieval path
