# Common Experiment Configuration

## Project

Diabetic Retinopathy Severity Classification using Deep Learning

## Dataset

DDR Dataset

## Classes

- 0 - No Diabetic Retinopathy
- 1 - Mild
- 2 - Moderate
- 3 - Severe
- 4 - Proliferative Diabetic Retinopathy

## Common Dataset Split

All models must use the shared `ddr_common_split.csv`.

Do not create a new train, validation, or test split.

- Training: 70%
- Validation: 15%
- Testing: 15%

## Random Seed

42

## Image Size

224 x 224 pixels

## Batch Size

32

## Data Augmentation

Apply only to the training dataset:

- Horizontal Flip
- Random Rotation: 0.05
- Random Zoom: 0.10
- Random Contrast: 0.10

Do not apply augmentation to validation or test data.

## Class Imbalance

Use the shared `class_weights.json` file.

## Models

- Custom CNN
- ResNet50
- MobileNetV2
- EfficientNetB0

## Evaluation Metrics

All models must report:

- Accuracy
- Macro Precision
- Macro Recall
- Macro F1-Score
- ROC-AUC
- Quadratic Weighted Kappa
- Confusion Matrix

## Test Dataset Rule

The test dataset must remain unseen during training and hyperparameter tuning.

Use the test dataset only for the final evaluation.

## Common Input

All models should use input images of size:

224 x 224 x 3
