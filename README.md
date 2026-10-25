# Phase 1: Single-View Faster R-CNN Baseline

## Overview
This phase establishes the empirical baseline for the thesis by training a standard single-view object detector on the VinDr-Mammo dataset. The goal is to quantify exactly where and by what margin 2D spatial models fail when analyzing dense breast tissue, specifically focusing on false-positive generation.

## Architecture & Setup
* **Model:** Faster R-CNN with a ResNet-50 FPN backbone.
* **Dataset:** 20,000 converted PNG images from the VinDr-Mammo dataset (80/20 train/val split).
* **Environment:** Google Colab Pro (A100/V100 GPU).
* **Framework:** PyTorch & Torchvision.

## Key Scripts
* **`Faster_RCNN_Baseline.ipynb`**: The complete, resumable training pipeline. Includes:
  * Automated DICOM to PNG conversion and Google Drive backup.
  * Custom PyTorch DataLoader for handling extreme scale variance in mammography lesions.
  * Training loop with Stochastic Gradient Descent (SGD).
  * Evaluation metrics generation (mAP@0.50 and FPPI).
  * Visualization generation (Loss curves and bounding box predictions).

## Empirical Results
The baseline model demonstrated that while a standard Faster R-CNN can extract raw features natively, it severely lacks structural disambiguation.
* **mAP@0.50:** 0.0314
* **FPPI (False Positives Per Image):** 0.0481

These metrics actively demonstrate the "alarm fatigue" of 2D models classifying overlapping healthy tissue as abnormalities, directly justifying the transition to the multi-view cross-attention architectures explored in **Phase 2**. 

## Usage
To reproduce these baseline metrics:
1. Ensure your VinDr-Mammo dataset annotations (`finding_annotations.csv`) and images are accessible.
2. Open `Faster_RCNN_Baseline.ipynb` in Google Colab.
3. Update the `base_drive_dir` path to point to your dataset location.
4. Run all cells sequentially.
