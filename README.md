# Dual-View Cross-Attention Networks for Mammography Lesion Localization and BI-RADS Classification
**Master's Thesis Project — KTH Royal Institute of Technology & Stockholm University**

This repository contains the codebase for my Master's thesis investigating the application of dual-view cross-attention mechanisms in full-field digital mammography (FFDM). The primary objective is to resolve single-view projection ambiguity—where overlapping fibroglandular tissue produces false positives—by enforcing ipsilateral spatial correspondence between Cranio-Caudal (CC) and Medio-Lateral Oblique (MLO) planes.

## Project Architecture & Roadmap
The research is structured into three sequential phases to rigorously evaluate the necessity and performance of cross-attention in multi-view medical imaging.

### 📁 [Phase 1: Pipeline & Single-View Baseline](./Phase-1-Single-View-Baseline)
* **Objective:** Establish the empirical baseline for the project by training a standard single-view object detector (Faster R-CNN) on normalized mammography scans.
* **Status:** ✅ Completed
* **Key Focus:** Preprocessed the high-resolution VinDr-Mammo DICOMs into standard normalized formats with bounding-box coordinate re-scaling. Benchmarked baseline localization (mAP, FROC-AUC) and highlighted the high false-positive rate inherent to single-view analysis.

### 📁 Phase 2: Dual-View Cross-Attention Module (In Progress)
* **Objective:** Develop a dual-branch backbone where CC and MLO feature maps interact directly.
* **Architecture:** Formulating the cross-attention along the anterior-posterior axis so that spatial tokens in the CC view explicitly query candidate regions along the corresponding slice in the MLO view.
* **Outputs:** Dual prediction heads for lesion-level bounding-box regression and global breast-level BI-RADS classification (1–5).

### 📁 Phase 3: Empirical Rigor & Fairness Evaluation (Upcoming)
* **Objective:** Perform robust ablation studies and algorithmic fairness checks.
* **Metrics:** Isolating the cross-attention module's performance against independent dual-branch ensembles (DBE) and the single-view baseline.
* **Stratification:** Evaluating performance across all BI-RADS breast density categories to test the model's robustness against severe tissue-masking effects. 

## Dataset
This project utilizes the [VinDr-Mammo Dataset](https://physionet.org/content/vindr-mammo/1.0.0/), consisting of 20,000 mammography images with radiologist-annotated bounding boxes and BI-RADS classifications.

## License
MIT License. See `LICENSE` for more information.
