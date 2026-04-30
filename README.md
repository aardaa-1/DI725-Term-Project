# DI725 Term Project -  FLAVA Remote Sensing Classification

This repository contains the Phase 2 implementation for the DI725 Transformers and Attention Based Deep Networks term project.

## Research Question

Does adding textual information improve remote sensing image classification performance compared to image only inputs?

## Project Summary

This project investigates whether textual information improves remote sensing image classification performance. A FLAVA based multimodal transformer is used to compare two experimental settings:

1. Image only classification baseline
2. Image+text multimodal classification

The main goal of Phase 2 is to obtain preliminary benchmarking results and compare both settings using classification metrics and inference speed.

## Dataset

The dataset is not included in this repository. Large files such as images, masks, captions, checkpoints, and model weights are excluded from version control.

The notebook expects the dataset to be available through the configured Google Drive path.

Expected dataset structure:

```text
data/
├── images/
├── masks/
└── captions.csv
```

The dataset contains true color remote sensing images, segmentation masks, and generated captions. The segmentation masks provide class composition information for the following classes:

  Tree
  Shrub
  Grass
  Crop
  Built up
  Barren
  Water

## Data Leakage Prevention

In Phase 1, the `hybrid_gemma3-4b` caption column was initially used. However, this column contains explicit class percentage information, which may cause data leakage.

For Phase 2, caption columns containing explicit class percentages are avoided. The selected text column is:

```text
vision_qwen3-vl-8b
```

This helps make the image+text experiment more reliable for evaluating whether textual descriptions improve classification performance.

## Phase 2 Benchmark Setup

For Phase 2, the benchmark is conducted on the three dominant classes:

  -Grass
  -Tree
  -Crop

This provides a controlled preliminary benchmark while reducing instability caused by rare classes. The full 7 class classification setup is planned for Phase 3 with class imbalance handling and additional ablation experiments.

## Metrics

The experiments will compare image only and image+text models using:

  -Accuracy
  -Macro F1 score
  -Weighted F1 score
  -Per class classification metrics
  -Confusion matrix
  -Inference speed

Inference speed is included to evaluate the computational cost of adding textual information to the image only baseline.

## Experiment Tracking

Weights & Biases is configured as optional experiment tracking. It is disabled by default in the notebook to avoid login or permission issues during execution.

GitHub is used for version control of the codebase.

## Repository Structure

```text
DI725 Term Project/
├── DI725_TermProject_2740926_Notebook.ipynb
├── README.md
├── requirements.txt
└── .gitignore
```

## How to Run

1. Install dependencies:

```bash
pip install -r requirements.txt
```

2. Make sure the dataset is available in the configured Google Drive path.

3. Open and run the notebook:

```text
DI725_TermProject_2740926_Notebook.ipynb
```

## Notes

The dataset, model checkpoints, and large output files are intentionally excluded from this repository. This repository is used to track the project code, configuration, documentation, and reproducibility files.
