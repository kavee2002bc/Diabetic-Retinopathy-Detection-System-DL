# Diabetic Retinopathy Detection System using Deep Learning

## 1. Project Overview

This project focuses on the automated classification of Diabetic Retinopathy (DR) from retinal fundus images using supervised deep learning.

Diabetic Retinopathy is a diabetes-related eye disease that can lead to vision impairment and blindness. Early detection and classification of disease severity can support timely clinical assessment.

The objective of this project is to develop and compare multiple deep learning models for classifying retinal images into five Diabetic Retinopathy severity classes.

## 2. Classification Classes

The dataset contains five classes:

| Class | Description |
|------:|-------------|
| 0 | No DR |
| 1 | Mild DR |
| 2 | Moderate DR |
| 3 | Severe DR |
| 4 | Proliferative DR |

## 3. Deep Learning Models

The project implements and compares four different deep learning architectures:

- Custom CNN
- ResNet
- MobileNet
- EfficientNetB0

Each model is implemented and evaluated using the same dataset and common train/validation/test split to support a fair comparison.

### Group Model Allocation

| Member | Model |
|---|---|
| Kaveesha | Custom CNN |
| Rashini | ResNet |
| Piyumi | MobileNet |
| Lakmi | EfficientNetB0 |

## 4. Dataset

The project uses the DDR (Diabetic Retinopathy) dataset.

The dataset contains retinal fundus images labelled according to Diabetic Retinopathy severity.

The project uses a common dataset split:

- Training set: 8,765 images
- Validation set: 1,878 images
- Test set: 1,879 images

The test set is kept separate and is used only for final evaluation.

### Dataset Access

The dataset is not included directly in this GitHub repository because of its large file size.

To run the notebooks:

1. Obtain the DDR dataset.
2. Extract the dataset.
3. Update the dataset path in the notebook if required.
4. Use the provided `ddr_common_split.csv` file to maintain the common train/validation/test split.

## 5. Dataset Split

A common split CSV file is used by all models:

`ddr_common_split.csv`

The CSV contains:

- `id_code`
- `diagnosis`
- `filepath`
- `exists`
- `split`

The predefined split is used instead of creating a new random train/test split for each model.

## 6. Preprocessing

The retinal images are processed before being passed to the deep learning models.

Main preprocessing steps include:

- Image resizing
- RGB image conversion
- Model-specific input preprocessing
- Training data augmentation
- Validation and test data kept without augmentation

For EfficientNetB0, images are resized to:

`224 x 224`

Training augmentation includes:

- Rotation
- Width shift
- Height shift
- Zoom
- Horizontal flipping

The validation and test datasets are not augmented.

## 7. Class Imbalance

The dataset contains an unequal number of images across the five classes.

To reduce the effect of class imbalance, class weights are calculated using the training set and applied during model training.

For the EfficientNetB0 model, the class weights are:

| Class | Class Name | Training Samples | Weight |
|------:|------------|-----------------:|-------:|
| 0 | No DR | 4386 | 0.3997 |
| 1 | Mild DR | 441 | 3.9751 |
| 2 | Moderate DR | 3134 | 0.5593 |
| 3 | Severe DR | 165 | 10.6242 |
| 4 | Proliferative DR | 639 | 2.7433 |

## 8. EfficientNetB0 Implementation

The EfficientNetB0 model uses ImageNet pretrained weights.

The pretrained convolutional base is initially frozen and a classification head is added.

Architecture:

- EfficientNetB0 pretrained base
- Global Average Pooling
- Dropout (0.3)
- Dense layer (128 units, ReLU)
- Dropout (0.2)
- Output Dense layer (5 units, Softmax)

### Training Configuration

| Parameter | Value |
|---|---|
| Input Size | 224 × 224 × 3 |
| Batch Size | 32 |
| Optimizer | Adam |
| Initial Learning Rate | 1e-5 |
| Loss Function | Categorical Crossentropy |
| Output Activation | Softmax |
| Hidden Activation | ReLU |
| Maximum Epochs | 15 |
| Random Seed | 42 |
| Number of Classes | 5 |

### Training Callbacks

The following callbacks are used:

- EarlyStopping
- ReduceLROnPlateau
- ModelCheckpoint

The best EfficientNetB0 model is selected using validation loss.

## 9. Evaluation Metrics

The models are evaluated using multiple classification metrics:

- Accuracy
- Precision
- Recall
- F1-score
- ROC-AUC
- Confusion Matrix

These metrics provide a broader evaluation than accuracy alone, particularly because the dataset is class-imbalanced.

## 10. EfficientNetB0 Results

The EfficientNetB0 model was evaluated on the held-out test set containing 1,879 images.

| Metric | Result |
|---|---:|
| Test Accuracy | 51.30% |
| Weighted Precision | 63.39% |
| Weighted Recall | 51.30% |
| Weighted F1-score | 52.64% |
| Macro ROC-AUC | 0.8121 |
| Weighted ROC-AUC | 0.7816 |

Per-class results are available in:

`EfficientNetB0_Results/classification_report.csv`

The confusion matrix and ROC curves are also included in the results folder.

## 11. Repository Structure

```text
Diabetic-Retinopathy-Detection-System-DL/
│
├── README.md
│
├── ddr_common_split.csv
│
├── IT23177246_EfficientNetB0_DDR.ipynb
│
├── EfficientNetB0_Results/
│   ├── class_weights.csv
│   ├── classification_report.csv
│   ├── confusion_matrix.csv
│   ├── confusion_matrix.png
│   ├── final_test_metrics.csv
│   ├── model_complexity.txt
│   ├── README.txt
│   ├── roc_curves.png
│   ├── test_predictions.csv
│   ├── training_history.csv
│   └── training_history.png
│
└── Other model notebooks
    ├── Custom CNN
    ├── ResNet
    └── MobileNet
