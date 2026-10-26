# Phase 1 Baseline: Single-View Mammography Lesion Localization

This repository contains the Phase 1 baseline implementation and visualization scripts for the master's thesis:  
**Dual-View Cross-Attention Networks for Mammography Lesion Localization and BI-RADS Classification**.

## Project Context
The code in this repository establishes the performance limits of standard 2D object detection architectures (Faster R-CNN with a ResNet-50-FPN backbone) when applied to single-view mammography scans. Single-view analysis inherently suffers from overlapping tissue ambiguity, making it highly difficult for conventional models to confidently separate true lesions from dense glandular tissue.

This baseline confirms that structural limitation, achieving a **mAP@0.50 of 0.0234** and an **FPPI of 0.0350**. 

The documented failure of this single-view approach serves as the academic justification for **Phase 2**, which introduces a Dual-View Cross-Attention mechanism to geometrically correlate Cranio-Caudal (CC) and Mediolateral Oblique (MLO) views.

## Repository Contents
* `visualize_baseline.py`: A complete Google Colab extraction, inference, and visualization pipeline. Generates an A2-formatted qualitative comparison highlighting the baseline's low-confidence predictions.
* `faster_rcnn_baseline.pth`: The saved model weights trained on the VinDr-Mammo dataset (configured for 36 target classes).

## Visualizing Failure Modes
To effectively demonstrate the baseline's struggle with ambiguous features, `visualize_baseline.py` bypasses PyTorch's default internal confidence filter (`box_score_thresh=0.0`). This forces the model to output all generated bounding boxes, no matter how low the confidence score. 

The script generates a 3-way side-by-side plot designed for poster presentations:
1. **Threshold > 0.15**: Demonstrates standard missed detections (false negatives).
2. **Threshold > 0.02**: Demonstrates scattered, noisy false positives.
3. **Top 3 Forced Guesses**: Shows the model's highest-ranked predictions to highlight peak confidence limits.

## Execution Instructions
1. Upload `visualize_baseline.py` and `faster_rcnn_baseline.pth` to your Google Colab environment.
2. Ensure your VinDr dataset annotations and image ZIP archive are mounted via Google Drive.
3. Run the script. The script bypasses full-archive extraction by reading the ZIP directly to locate a confirmed ground-truth lesion.
4. The output `detection_comparison_poster.jpg` will automatically download upon completion.

---
*Note: This code is open-sourced prior to final thesis completion in compliance with KTH Royal Institute of Technology's open-source sharing policies. The final manuscript will be submitted prior to the formal defense.*
