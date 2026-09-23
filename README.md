# Custom CNN - Diabetic Retinopathy Severity Classification

## Overview

This branch contains the implementation and evaluation of the **Custom Convolutional Neural Network (CNN)** developed for the SE4050 Deep Learning group assignment.

The objective of this model is to classify Diabetic Retinopathy severity from retinal fundus images using supervised deep learning.

The model is trained and evaluated using the shared DDR dataset split defined by the group.

---

## Classification Task

The model performs five-class classification.

| Label | Class |
|------|------|
| 0 | No Diabetic Retinopathy |
| 1 | Mild |
| 2 | Moderate |
| 3 | Severe |
| 4 | Proliferative Diabetic Retinopathy |

---

## Dataset

The project uses the DDR Diabetic Retinopathy dataset.

The complete dataset is not stored in this GitHub repository because of its large file size.

This branch uses the common dataset split provided in:

```text
data/ddr_common_split.csv
