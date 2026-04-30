# DI725 Term Project - FLAVA Remote Sensing Classification

This repository contains the implementation files for the DI725 Transformers and Attention Based Deep Networks term project.

## Research Question

Does adding textual information improve remote sensing image classification performance compared to image only inputs?

## Project Summary

This project investigates whether textual information improves remote sensing image classification performance. A FLAVA based multimodal transformer is used to compare two experimental settings:

1. "Image Only" classification baseline
2. "Image + Text" multimodal classification model

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

- Tree
- Shrub
- Grass
- Crop
- Built-up
- Barren
- Water

## Data Leakage Prevention

In Phase 1, the `hybrid_gemma3-4b` caption column was initially used. However, this column contains explicit class percentage information, which may cause data leakage because the text can directly reveal the target class.

For Phase 2, caption columns containing explicit class percentages are avoided. The selected text column for the main Phase 2 benchmark is:

```text
vision_qwen3-vl-8b
```

A leakage check is included in the notebook to compare caption columns and verify that the selected Phase 2 text column does not contain explicit percentage-based class information.

## Phase 2 Benchmark Setup

For Phase 2, the main benchmark is conducted on the three dominant classes:

- Grass
- Tree
- Crop

This setup uses 9,543 samples from the full dataset pool and avoids the earlier random 1000 sample subset. It provides a controlled preliminary benchmark while reducing instability caused by very rare dominant classes.

## Models

The Phase 2 experiments compare two FLAVA based models:

1. "Image Only" baseline  
   - Uses only image inputs.
   - Serves as the baseline model.

2. "Image + Text" fusion model  
   - Uses image, text, and multimodal FLAVA representations.
   - Uses  textual descriptions as additional input.

Both models are trained and evaluated using the same train, validation, and test splits.

## Metrics

The experiments compare the models using:

- Accuracy
- Macro F1 score
- Weighted F1 score
- Per class precision, recall, and F1 score
- Confusion matrix
- Inference time
- Samples per second
- Milliseconds per sample

Macro F1 score is emphasized because the dataset is imbalanced and macro F1 gives equal importance to each class.

## Main Phase 2 Findings

In the controlled top 3 benchmark, the "Image Only" and "Image + Text" models achieved very similar test performance.

The "Image + Text" model achieved slightly higher test accuracy and weighted F1 score, while the "Image Only" model achieved slightly higher macro F1 score. The inference speed comparison showed that adding text increased computational cost.

Overall, Phase 2 suggests that textual descriptions provide comparable predictive performance, but they do not yet provide a clear improvement over the image only baseline relative to their additional inference cost.

## Experiment Tracking

GitHub is used for code version control and reproducibility.

Weights & Biases is configured as optional experiment tracking in the notebook. It may be disabled before final submission to avoid login or permission issues when the notebook is rerun.

## Repository Structure

```text
DI725-Term-Project/
├── notebooks/
│   ├── phase1/
│   │   └── DI725_TermProject_Phase1.ipynb
│   ├── phase2/
│   │   └── DI725_TermProject_Phase2.ipynb
│   ├── phase3/
│   └── phase4/
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

3. Open and run the relevant notebook:

```text
notebooks/phase1/DI725_TermProject_Phase1.ipynb
notebooks/phase2/DI725_TermProject_Phase2.ipynb
```

4. For Phase 2, run the notebook from top to bottom. The Phase 1 PoC cells are kept unchanged, and the Phase 2 improvements start under the "PHASE 2" section.

## Notes

The dataset, model checkpoints, trained weights, W&B local logs, and large output files are intentionally excluded from this repository.

This repository is used to track the project code, configuration, documentation, and reproducibility files.
