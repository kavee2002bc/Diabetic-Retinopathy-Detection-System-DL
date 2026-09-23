# Diabetic Retinopathy Detection System using Deep Learning

## Project Overview

This project is developed for the SE4050 – Deep Learning module.

The objective of this project is to classify the severity of Diabetic Retinopathy from retinal fundus images using supervised deep learning techniques.

The project compares four different deep learning architectures under the same experimental conditions.

## Problem Type

- Supervised Deep Learning
- Image Classification
- Multi-Class Classification

## Dataset

We use the DDR (Diabetic Retinopathy Dataset) for this project.

The dataset contains retinal fundus images classified into five Diabetic Retinopathy severity levels.

### Classes

| Label | Class |
|------|------|
| 0 | No Diabetic Retinopathy |
| 1 | Mild |
| 2 | Moderate |
| 3 | Severe |
| 4 | Proliferative Diabetic Retinopathy |

The dataset contains approximately 12,522 retinal images used for the five-class classification task.

The complete image dataset is not uploaded to this GitHub repository due to its large size.

Dataset access instructions are provided separately for the project members.

## Deep Learning Models

The following four deep learning architectures are implemented and compared:

1. Custom CNN
2. ResNet50
3. MobileNetV2
4. EfficientNetB0

## Experimental Configuration

All models use the same training, validation and testing data split to ensure a fair comparison.

- Image Size: 224 × 224
- Random Seed: 42
- Batch Size: 32
- Number of Classes: 5
- Dataset Split: 70% Training, 15% Validation, 15% Testing
- Class Imbalance Handling: Class Weights
- Optimizer: Adam
- Evaluation performed using the same test dataset

## Data Augmentation

The following augmentation techniques are applied to the training dataset:

- Horizontal Flip
- Small Rotation
- Zoom
- Contrast Adjustment

Augmentation is applied only to the training dataset.

## Evaluation Metrics

The models are evaluated using:

- Accuracy
- Precision
- Recall
- Macro F1-Score
- ROC-AUC
- Quadratic Weighted Kappa (QWK)
- Confusion Matrix

## Repository Structure

```text
Diabetic-Retinopathy-Detection-System-DL/
│
├── data/
│   └── ddr_common_split.csv
│
├── config/
│   ├── class_weights.json
│   └── common_experiment_config.md
│
├── notebooks/
│   ├── 01_DDR_Dataset_EDA.ipynb
│   ├── 02_Custom_CNN.ipynb
│   ├── 03_ResNet50.ipynb
│   ├── 04_MobileNetV2.ipynb
│   └── 05_EfficientNetB0.ipynb
│
├── results/
│   ├── cnn/
│   ├── resnet50/
│   ├── mobilenetv2/
│   └── efficientnetb0/
│
├── README.md
├── requirements.txt
└── .gitignore
