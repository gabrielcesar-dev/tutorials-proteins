# Antimicrobial Peptide Design Tutorial

This repository contains a tutorial for designing antimicrobial peptides using the Molecular Reinforcement Learning (MRL) framework. The tutorial provides an end-to-end workflow for peptide design and optimization.

## Overview

Antimicrobial peptides are a family of peptides that can kill bacteria, making them of interest for antibiotics and anticancer therapeutics. This tutorial walks through:

1. Loading and preprocessing peptide datasets.
2. Training a model to predict antimicrobial activity.
3. Fine-tuning a pretrained language model for peptide generation.
4. Using reinforcement learning to optimize peptide sequences for desired properties.

## Key Features

- **Dataset**: The dataset used in this tutorial comes from the [AMPlify](https://github.com/bcgsc/AMPlify) repository, which contains ~8300 short peptides classified as antimicrobial or not.
- **Model Training**: A convolutional neural network (CNN) is trained to classify peptides for antimicrobial activity.
- **Fine-Tuning**: A pretrained language model (`LSTM_LM_Small_Swissprot`) is fine-tuned to generate antimicrobial peptides.
- **Reinforcement Learning**: The PPO algorithm is used to optimize sequences, with rewards based on antimicrobial activity and optional stability metrics.
- **Chemical Filters**: Rules and filters are applied to constrain the generated sequences for quality and realism.

## Workflow

### 1. Model Training
The tutorial trains a CNN with an MLP head to classify peptides as antimicrobial or not. The training and validation datasets are split as follows:
- **Training Set**: 95% of the data.
- **Validation Set**: 5% of the data.

### 2. Fine-Tuning
The pretrained language model is fine-tuned specifically for generating antimicrobial peptides. The model is trained on sequences labeled as antimicrobial.

### 3. Reinforcement Learning
Reinforcement learning is used to further optimize peptide sequences:
- **Policy Gradient Loss**: PPO is used as the policy gradient loss.
- **Rewards**:
  - A predictive CNN model provides antimicrobial activity scores.
  - An optional stability metric derived from a pretrained protein transformer model.

### 4. Chemical Space Filtering
To ensure realistic sequences, filters are applied based on:
- Validity rules.
- Residue frequency constraints.
- Toxicity considerations (e.g., limiting arginine content).

### 5. Samplers
Multiple samplers are implemented for generating new sequences:
- Sampling from the main model.
- Sampling from the baseline model.
- High-scoring sample selection.
- Token swap strategies.

## Getting Started

### Prerequisites
- Python 3.7 or later
- Packages required: `torch`, `pandas`, `scikit-learn`, `matplotlib`, [ESM](https://github.com/facebookresearch/esm), and other dependencies listed in the tutorial.

### Installation
Install the `mrl` library from PyPI:
```bash
pip install -U mrl-pypi
```

### Running the Tutorial
1. Clone the repository:
   ```bash
   git clone https://github.com/gabrielcesar-dev/tutorials-proteins.git
   cd mrl/nbs/tutorials
   ```
2. Open and run the `tutorials.proteins.amp.ipynb` notebook using Jupyter or a compatible environment.

### Example Outputs
- **Training Results**: Loss and accuracy metrics for the predictive model.
- **Validation Results**: ROC curves and AUC scores for antimicrobial activity.
- **Generated Sequences**: Optimized peptide sequences with high antimicrobial activity scores.

## Additional Notes

- **Runtime Environment**: The tutorial is optimized for systems with GPU support but can also run on CPU (with slower performance).
- **Optional Stability Reward**: Pretrained protein transformer models can be used to include stability as a reward metric.

## References
- [AMPlify Dataset](https://github.com/bcgsc/AMPlify)
- [ESM Protein Transformer](https://github.com/facebookresearch/esm)
- [Antimicrobial Peptide Toxicity Study](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5625148/)

## License
This project is licensed under the MIT License. See the LICENSE file for details.

## Acknowledgments
Thanks to the contributors of the [MRL Framework](https://github.com/DarkMatterAI/mrl) for developing the tools and libraries used in this tutorial.

---

Let me know if you'd like me to adjust or expand any sections!
