# ResNet50 – Diabetic Retinopathy Grading

This folder contains the ResNet50 implementation for the Diabetic Retinopathy Detection System (Deep Learning – SE4050 Assignment). This is one of four deep-learning architectures being compared as part of the group's supervised deep-learning project.

## 1. Problem Definition

The task is a **5-class image classification problem**: grading the severity of Diabetic Retinopathy (DR) from retinal fundus images into classes 0–4 (No DR, Mild, Moderate, Severe, Proliferative DR).

## 2. Dataset

- **Source:** DDR (Diabetic Retinopathy) grading dataset
- **Split file:** `ddr_common_split.csv` — a shared, fixed train/validation/test split used across **all four models** in this project to ensure fair comparison
- **Classes:** 5 (0–4, ordinal severity grading)
- **Image size used:** 224 x 224 x 3
- **Note:** The dataset exhibits significant class imbalance (Class 0 and Class 2 dominate; Classes 1 and 3 are minority classes)

## 3. Model Architecture

- **Backbone:** ResNet50 (pretrained on ImageNet, `include_top=False`)
- **Preprocessing:** `tf.keras.applications.resnet50.preprocess_input`
- **Custom head:**
  - GlobalAveragePooling2D
  - Dropout (0.4)
  - Dense (128, ReLU)
  - Dropout (0.3)
  - Dense (5, Softmax)
- **Data augmentation:** RandomFlip (horizontal), RandomRotation (0.05), RandomZoom (0.10), RandomContrast (0.10)

## 4. Training Strategy

Training was carried out in **two phases**, following a transfer-learning + fine-tuning approach.

### Phase 1 – Frozen Backbone
- Backbone frozen (`base_model.trainable = False`)
- Only the classification head trained
- Optimizer: Adam (lr = 1e-3)
- 10 epochs

### Phase 2 – Fine-Tuning
- Last ~60 layers of the backbone unfrozen (BatchNormalization layers kept frozen to preserve stable statistics)
- Optimizer: Adam (lr = 2e-5)
- Soft class weights applied (square root of balanced class weights) to reduce over-correction toward minority classes
- Callbacks: EarlyStopping (patience = 4, restore best weights), ReduceLROnPlateau (factor = 0.5, patience = 2), ModelCheckpoint
- Up to 15 epochs (early-stopped)

### Model Iterations

Three versions were trained while diagnosing and fixing issues:

| Version | Change | Purpose |
|---|---|---|
| v1 | Baseline fine-tuning | Initial fine-tuning pass |
| v2 | BatchNorm layers frozen during fine-tuning | Fixed unstable fine-tuning caused by BN statistics updating |
| v3 | Soft (square root) class weights | Reduced over-prediction of minority classes seen in v1/v2 |

Model selection was performed using the validation set only (not the test set), consistent with the assignment requirement that the test set remain unseen until final evaluation.

## 5. Results (Test Set – Final Model: v3)

| Metric | Value |
|---|---|
| Test Accuracy | 75.15% |
| Test Loss | 0.668 |
| Precision (macro) | 0.58 |
| Recall (macro) | 0.55 |
| F1-score (macro) | 0.55 |
| AUC (OvR, macro) | 0.895 |
| Quadratic Weighted Kappa (QWK) | 0.76 |
| Inference time | ~16 ms per image (T4 GPU) |

Full classification report, confusion matrices (raw and normalized), ROC curves, and training curves are provided alongside this notebook.

## 6. Files in this Folder

- ResNet50.ipynb — Full training and evaluation notebook
- resnet50_v3_results.json — Final metrics and config summary
- resnet50_v1_v2_v3_comparison.csv — Comparison across model iterations
- resnet50_val_model_selection.csv — Validation-based model selection results
- resnet50_v3_confusion_matrix.png — Confusion matrix (raw counts)
- resnet50_v3_confusion_matrix_normalized.png
- resnet50_v3_roc_curves.png — One-vs-rest ROC curves per class
- resnet50_v3_training_curves.png — Accuracy and loss curves (Phase 1 + Phase 2)
- resnet50_v3_classification_report.csv

## 7. How to Reproduce

1. Open ResNet50.ipynb in Google Colab
2. Mount Google Drive and ensure ddr_common_split.csv and the DDR image dataset are accessible
3. Run cells in order: dataset loading, augmentation, class weights, model definition, Phase 1 training, Phase 2 training, evaluation
4. SEED is set to 42 at the top of the notebook for reproducibility

## 8. Key Findings and Limitations

- Model performs strongly on Class 0 (recall 0.93) and Class 4 (recall 0.68)
- Class 1 and Class 3 (minority classes) remain difficult to classify, largely due to severe class imbalance and visual similarity to adjacent severity grades
- Most misclassifications occur between adjacent severity classes rather than distant ones, which is reflected in the relatively high QWK (0.76) despite moderate raw accuracy
- Further improvement directions: ordinal regression/decoding, higher input resolution, additional minority-class augmentation

## 9. Dataset Citation

(Add the exact dataset source, creator, license, and URL here)
