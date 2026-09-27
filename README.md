# Diabetic Retinopathy Detection System – ResNet50 Branch

This branch contains the **ResNet50** implementation for the Diabetic Retinopathy Detection System (SE4050 – Deep Learning Assignment). ResNet50 is one of four deep-learning architectures being implemented and compared across the group as part of this supervised deep-learning project.

## Contents

- **Notebook:** [`results/resnet50/ResNet50.ipynb`](results/resnet50/ResNet50.ipynb) — full training and evaluation pipeline
- **Detailed documentation and results:** [`results/resnet50/README.md`](results/resnet50/README.md)

## Summary

- **Task:** 5-class Diabetic Retinopathy severity grading (classes 0–4)
- **Architecture:** ResNet50 (ImageNet pretrained), transfer learning + two-phase fine-tuning
- **Final model (v3) test performance:**
  - Accuracy: 75.15%
  - F1-score (macro): 0.55
  - AUC (OvR, macro): 0.895
  - Quadratic Weighted Kappa (QWK): 0.76

See [`results/resnet50/README.md`](results/resnet50/README.md) for full architecture details, training strategy, dataset information, results, and reproduction instructions.
