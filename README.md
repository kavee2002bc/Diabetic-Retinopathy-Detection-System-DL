# EfficientNetB0 - Diabetic Retinopathy Classification

## Student Contribution

- Student Name: A.S.P.L.T Pushpakumara
- Student ID: IT23177246
- Model: EfficientNetB0
- Task: Five-Class Diabetic Retinopathy Classification

## Overview

This module implements an EfficientNetB0-based deep learning model for diabetic retinopathy classification using the DDR dataset.

The model performs five-class classification of retinal fundus images into the following categories:

1. No DR
2. Mild DR
3. Moderate DR
4. Severe DR
5. Proliferative DR

## Dataset Split

The common dataset split used for the project contains:

- Training set: 8,765 images
- Validation set: 1,878 images
- Test set: 1,879 images

The test set was kept separate and used only for final model evaluation.

The dataset images are not included in this repository because of the large dataset size.

## Model Architecture

EfficientNetB0 pretrained with ImageNet weights was used as the feature extraction backbone.

The classification head consists of:

- Global Average Pooling
- Dropout (0.3)
- Dense layer with 128 units
- ReLU activation
- Dropout (0.2)
- Dense output layer with 5 units
- Softmax activation

The pretrained EfficientNetB0 backbone was frozen during the training stage.

## Input Configuration

- Image size: 224 × 224 × 3
- Batch size: 32
- Number of classes: 5
- Random seed: 42

## Data Augmentation

Data augmentation was applied only to the training set:

- Rotation range: 10 degrees
- Width shift: 0.05
- Height shift: 0.05
- Zoom range: 0.10
- Horizontal flip: Enabled

Validation and test images were not augmented.

## Class Imbalance Handling

The training dataset contains an imbalanced distribution across the five diabetic retinopathy classes.

Balanced class weights were calculated using the training set and applied during model training to reduce the effect of class imbalance.

## Training Configuration

- Optimizer: Adam
- Learning rate: 1e-5
- Loss function: Categorical Crossentropy
- Batch size: 32
- Pretrained weights: ImageNet

### Callbacks

The following callbacks were used:

- EarlyStopping
- ModelCheckpoint
- ReduceLROnPlateau

EarlyStopping monitored validation loss with a patience of 5 epochs and restored the best model weights.

ReduceLROnPlateau monitored validation loss and reduced the learning rate when validation performance stopped improving.

## Evaluation Metrics

The model was evaluated on the unseen test set using:

- Accuracy
- Precision
- Recall
- F1-score
- ROC-AUC
- Confusion Matrix

Visual error analysis was also performed using misclassified test images.

## Test Results

The EfficientNetB0 model achieved:

- Test Accuracy: 43.69%
- Test Loss: 1.4295

### ROC-AUC Results

| Class | ROC-AUC |
|---|---:|
| No DR | 0.6762 |
| Mild DR | 0.4797 |
| Moderate DR | 0.4753 |
| Severe DR | 0.6304 |
| Proliferative DR | 0.7114 |

### Error Analysis

A total of 1,879 test images were evaluated.

- Misclassified images: 1,058
- Misclassification rate: 56.31%

Visual inspection of selected misclassified examples was performed to examine the types of classification errors produced by the model.

## Repository Files

- `IT23177246_EfficientNetB0_DDR_Diabetic_Retinopathy.ipynb` - Complete EfficientNetB0 implementation, training and evaluation notebook.
- `README.md` - Documentation for the EfficientNetB0 implementation.
- `requirements.txt` - Python dependencies.
- `config.txt` - Model and training configuration.

## Reproducibility

The notebook records the model architecture, preprocessing configuration, data augmentation settings, random seed, optimizer, learning rate, class-weighting strategy, callbacks and evaluation procedures used for the experiment.

## Dataset Access

The DDR dataset is not included in this repository because of its large size.


# EfficientNetB0 Results

This folder contains the final evaluation results and visualizations for the EfficientNetB0 diabetic retinopathy classification model.

The results were obtained using the held-out test set after model training.

## Included Results

- `efficientnetb0_metrics.csv` - Final test metrics
- `classification_report.csv` - Precision, recall, F1-score and support
- `confusion_matrix.png` - Confusion matrix
- `roc_curve.png` - One-vs-Rest ROC curves and AUC values
- `training_history.png` - Training and validation accuracy/loss
- `misclassified_examples.png` - Examples of incorrectly classified retinal images

The dataset should be obtained through the dataset source used by the project and placed in the required local/Google Drive path before running the notebook.

## Important Note

The test set was used only for final evaluation and was not used for model training or hyperparameter tuning.
