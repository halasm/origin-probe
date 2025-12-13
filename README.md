# Origin Probe: Phi-2 Agreement Bias Experiment

This repository implements a pretrained-only origin probe experiment on Microsoft Phi-2 to measure agreement bias in language models. The experiment compares model responses across neutral (undefined and ambiguous) and framed (case1 and case2) prompt conditions to quantify the extent to which pretrained models exhibit agreement bias.

## Overview

The origin probe is designed to distinguish between biases that originate from pretraining versus those introduced through reinforcement learning from human feedback (RLHF). By testing a pretrained-only model (Phi-2) on moral dilemma scenarios from the Moral Machine dataset, we measure whether the model shows increased agreement rates when prompts explicitly frame agreement with a particular choice, compared to neutral baselines.

## Data

The dataset is located at: `data/shared_responses_Phi-3.5-mini-instruct.csv`

See `data/DATA_SOURCE.md` for detailed provenance and citations.

## Installation

```bash
pip install -r requirements.txt
```

## Usage

1. Open `origin_probe_phi2.ipynb` in Jupyter
2. Run all cells from top to bottom

The notebook will:
- Load the Phi-2 model (automatically downloads from HuggingFace if needed)
- Load the Moral Machine dataset from `data/shared_responses_Phi-3.5-mini-instruct.csv`
- Run the experiment across multiple random seeds
- Generate results in the `results/` directory

## Output

The experiment produces two CSV files in `results/`:

- `summary.csv`: Main condition summary table with agreement rates, format adherence, and lifts vs neutral baselines
- `seed_summary.csv`: Per-seed aggregated metrics across all experimental conditions

## Reproducibility Notes

This experiment was originally run on a GPU cluster. It should run locally with a compatible GPU. If no GPU is available, users can reduce the number of scenarios (`N_SCENARIOS` variable in the notebook) to run on CPU, though this will increase runtime.

The experiment uses deterministic decoding (`do_sample=False`) to ensure reproducibility across runs with the same random seeds.

## Citations

If you use this code or dataset, please cite:

1. **Takemoto K (2024)** The Moral Machine Experiment on Large Language Models. *R. Soc. Open Sci.* **11**, 231393. https://doi.org/10.1098/rsos.231393

2. **Ahmad MSZ and Takemoto K (2025)** Large-Scale Moral Machine Experiment on Large Language Models. *PLoS One*, **20**, e0322776. https://doi.org/10.1371/journal.pone.0322776
 
We use the released dataset for scenario generation only; all modeling, prompting,
and analysis in this repository are original to this work.