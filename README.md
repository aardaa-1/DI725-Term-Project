# DI725 Term Project - FLAVA Remote Sensing Classification

This repository contains the implementation files for the DI725 Transformers and Attention Based Deep Networks term project.

## Research Question

Does adding textual information improve remote sensing image classification performance compared to image only inputs?

## Project Summary

This project investigates whether generated textual descriptions improve remote sensing image classification compared with image only inputs. A FLAVA based multimodal transformer is used to compare image only and image+text classification settings.

The final experiments extend the earlier benchmark to a full seven class remote sensing classification task. The study includes caption leakage checking, caption source ablation, shuffled caption sanity checking, per-class evaluation, rare class analysis, and inference cost comparison.

## Dataset

The dataset is not included in this repository. Large files such as images, masks, captions, checkpoints, model weights, and W&B logs are excluded from version control.

The notebook expects the dataset to be available through the configured Google Drive path.

Expected dataset structure:

```text
data/
├── images/
├── masks/
└── captions.csv
```

The dataset contains true color remote sensing images, segmentation masks, and generated captions. The segmentation masks provide class composition information for the following classes:

* Tree
* Shrub
* Grass
* Crop
* Built-up
* Barren
* Water

For the classification task, the dominant class in the segmentation-mask-based pixel distribution is used as the target label.

## Data Leakage Prevention

Caption columns are checked for possible leakage before training the multimodal models. Text based and hybrid caption columns may contain explicit class percentage or class-composition information. These columns are excluded from the main leakage-safe benchmark.

The final experiments use vision-based caption columns:

```text
vision_qwen3-vl-8b
vision_gemma3-4b
```

A shuffled Qwen caption setting is also used as a sanity check ablation.

## Final Experimental Setup

The final benchmark uses the full dataset of 10,000 samples with a stratified train-validation-test split:

* Train: 6,000 samples
* Validation: 2,000 samples
* Test: 2,000 samples

Four experimental settings are evaluated:

| ID | Experiment    | Description                                   |
| -- | ------------- | --------------------------------------------- |
| E1 | Image Only    | FLAVA image only baseline                     |
| E2 | Qwen Caption  | Image+text model using Qwen vision captions   |
| E3 | Gemma Caption | Image+text model using Gemma vision captions  |
| E4 | Shuffled Qwen | Image+text model using shuffled Qwen captions |

Class weighted cross entropy loss is used because the full seven class dataset is highly imbalanced.

## Metrics

The experiments compare the models using:

* Accuracy
* Balanced accuracy
* Macro F1 score
* Weighted F1 score
* Per-class precision, recall, and F1 score
* Rare-class macro F1
* Confusion matrix
* Inference time
* Milliseconds per sample

Macro F1 and rare class macro F1 are emphasized because the dataset is imbalanced.

## Main Findings

The final results show that adding textual information does not substantially improve overall accuracy. However, caption based models improve macro F1 and rare class macro F1 compared with the image only baseline.

The Gemma caption model achieves the best macro F1 and rare class macro F1. The rare class analysis shows that Built-up and Barren benefit more clearly from caption based models. However, the shuffled caption ablation also performs competitively for some classes, so the contribution of textual information should be interpreted carefully.

The inference cost analysis shows that image+text models are approximately 1.8 times more expensive during inference than the image only baseline.

## Experiment Tracking

Weights & Biases is configured as optional experiment tracking in the notebook. 

## Repository Structure

```text
DI725-Term-Project/
├── notebooks/
│   ├── phase1/
│   ├── phase2/
│   └── phase3/
├── reports/
│   ├── DI725_TermProjectReport__2740926.pdf
│   └── figures/
│       ├── fig1_per_class_f1_comparison.png
│       └── fig2_qualitative_examples.png
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

3. Open the final notebook:

```text
notebooks/phase3/DI725_TermProject_Notebook_2740926.ipynb
```

4. Run the notebook from top to bottom if the dataset paths are correctly configured.

## Notes

The dataset, model checkpoints, trained weights, W&B local logs, and large output files are intentionally excluded from this repository.

This repository is used to track the project code, configuration, documentation, report materials, and reproducibility files.
