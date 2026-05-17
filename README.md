# LLM and Loopholes

This project tests whether LLMs exploit an "answer anyway" loophole when they are uncertain or when a request is impossible to satisfy exactly. The experiments use real OpenAI API models on local benchmark slices from `SimpleQA`, `TruthfulQA`, and `HALoGEN` false-presupposition prompts.

Key findings:
- On impossible `HALoGEN` prompts, `forced_answer` caused both tested models to attempt an answer 100% of the time, versus 28.3% (`gpt-4.1`) and 31.7% (`gpt-5-mini`) under `abstain_allowed`.
- `gpt-5-mini` showed a strong knowledge-uncertainty tradeoff: on `SimpleQA`, incorrect answers dropped from 86.0% at baseline to 8.0% with abstention instructions, but rose to 90.0% under `forced_answer`.
- `gpt-4.1` was much less responsive to abstention prompting on factual QA, but it still fabricated heavily on impossible structured requests.
- The strongest evidence for loophole-like behavior came from impossible requests, not from ordinary misconception questions.

Reproduce:
```bash
source .venv/bin/activate
python -m research_workspace.run_experiments \
  --simpleqa-n 50 \
  --truthfulqa-n 50 \
  --halogen-impossible-n 60 \
  --halogen-possible-n 20 \
  --max-workers 6
```

Outputs:
- Full report: [REPORT.md](/workspaces/llm-loopholes-research-9e63-codex/REPORT.md)
- Plan: [planning.md](/workspaces/llm-loopholes-research-9e63-codex/planning.md)
- Experiment runner: [run_experiments.py](/workspaces/llm-loopholes-research-9e63-codex/src/research_workspace/run_experiments.py)
- Aggregate metrics: [aggregate_metrics.csv](/workspaces/llm-loopholes-research-9e63-codex/results/evaluations/aggregate_metrics.csv)
- Statistical tests: [statistical_tests.csv](/workspaces/llm-loopholes-research-9e63-codex/results/evaluations/statistical_tests.csv)
- Raw model outputs: [all_predictions.jsonl](/workspaces/llm-loopholes-research-9e63-codex/results/model_outputs/all_predictions.jsonl)
- Figures: [factual_benchmark_rates.png](/workspaces/llm-loopholes-research-9e63-codex/figures/factual_benchmark_rates.png), [halogen_false_presupposition_rates.png](/workspaces/llm-loopholes-research-9e63-codex/figures/halogen_false_presupposition_rates.png)

File structure:
- `datasets/`: local benchmark material
- `code/`: upstream benchmark repos used for reference
- `src/research_workspace/`: experiment code
- `results/`: raw outputs, config, aggregate tables
- `figures/`: report figures
