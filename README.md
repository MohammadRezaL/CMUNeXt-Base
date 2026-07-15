# CMUNeXt Boundary-Aware Breast Ultrasound Segmentation

> Research project extending **CMUNeXt** for lightweight boundary-aware breast ultrasound image segmentation.

## Overview

This project aims to improve the boundary quality of **CMUNeXt** while preserving its lightweight architecture. The research focuses on breast ultrasound lesion segmentation using the **BUSI dataset**, with particular attention to boundary-based evaluation metrics such as **HD95** and **ASSD**.

Rather than simply increasing Dice or IoU, the objective is to reduce catastrophic boundary errors and improve contour localization without significantly increasing computational complexity.

---

## Dataset

- **BUSI (Breast Ultrasound Images)**
- Image size: **256 × 256**
- Fixed dataset split:
  - Training: **452**
  - Validation: **195**

The dataset split remains identical throughout all experiments to ensure fair comparisons.

---

## Baseline

The starting point is the original **CMUNeXt** architecture.

Training configuration:

- Optimizer: SGD
- Learning rate: 0.01
- Batch size: 8
- Epochs: 300
- Seed: 41

---

# Research Progress

## ✅ Phase 1 — Baseline Reproduction

- Reproduced the original CMUNeXt training pipeline.
- Trained using the fixed BUSI split.
- Established the baseline for future comparisons.

---

## ✅ Phase 2 — Boundary Evaluation Framework

Implemented a unified evaluation pipeline including:

- Dice
- IoU
- Precision
- Recall
- Accuracy
- HD95
- ASSD
- Empty Predictions

The same evaluation pipeline is used for every experiment.

---

## ✅ Phase 3 — BoundaryDoU Loss

Replaced the original BCE + Dice loss with **BoundaryDoU Loss** while keeping every other training setting unchanged.

### Experimental Findings

Positive observations:

- Reduced mean ASSD
- Reduced prediction variance
- Fewer empty predictions
- Improved median HD95

Observed limitations:

- Mean HD95 increased slightly
- Several challenging lesions became under-segmented

---

## Qualitative Analysis

Detailed visual inspection revealed three different prediction behaviors.

### Type A

BoundaryDoU successfully detects lesions that are completely missed by the baseline.

### Type B

Both models fail on particularly difficult cases.

### Type C

The baseline predicts more complete lesion regions, while BoundaryDoU produces conservative (smaller) masks.

These observations suggest that the two models exhibit **complementary prediction behaviors** rather than one consistently outperforming the other.

---

## Threshold Analysis

A threshold sweep (0.30–0.70) was performed.

Findings:

- Lower thresholds reduced empty predictions.
- ASSD improved noticeably.
- HD95 remained largely unchanged.

This suggests that the observed boundary failures are not solely caused by threshold selection.

---

# Current Conclusion

BoundaryDoU changes the prediction characteristics of CMUNeXt rather than universally improving segmentation performance.

The experiments indicate:

- improved boundary consistency for many samples,
- reduced empty predictions,
- improved ASSD,
- but occasional severe under-segmentation.

The complementary behavior between BoundaryDoU and the baseline motivates the development of a multi-branch segmentation framework.

---

# Planned Work

- [x] Reproduce CMUNeXt
- [x] Boundary evaluation (HD95 / ASSD)
- [x] BoundaryDoU Loss
- [ ] Auxiliary Boundary Prediction Head
- [ ] BoundaryDoU + Boundary Head
- [ ] Lightweight Multi-Branch Fusion
- [ ] Complete ablation study
- [ ] Paper submission

---

# Research Goal

Develop a lightweight boundary-aware segmentation framework that

- improves HD95
- improves ASSD
- reduces catastrophic failures
- reduces empty predictions
- preserves the efficiency of CMUNeXt

---

## Repository Status

**Project Stage:** Active Research

This repository is under active development. New experiments, ablation studies, and model variants will be added as the research progresses.
