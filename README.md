# MobileNetV2 Results

This folder contains the training and evaluation results of the MobileNetV2 model for diabetic retinopathy severity classification.

## Model

MobileNetV2 using ImageNet-pretrained weights with transfer learning and fine-tuning.

## Classification Classes

| Label | Class |
|---:|---|
| 0 | No DR |
| 1 | Mild |
| 2 | Moderate |
| 3 | Severe |
| 4 | Proliferative DR |

## Input

224 × 224 RGB retinal fundus images.

## Training Strategy

- Data augmentation
- Class-weighted training
- Transfer learning
- Frozen-backbone training
- Fine-tuning
- Adam optimizer
- Early stopping
- Learning-rate reduction

## Dataset Split

The common team split from `ddr_common_split.csv` was used.

Train: 8,765 images  
Validation: 1,878 images  
Test: 1,879 images

## Final Test Results

| Metric | Result |
|---|---:|
| Accuracy | 0.5338 |
| Macro Precision | 0.4814 |
| Macro Recall | 0.5923 |
| Macro F1 | 0.4547 |
| ROC-AUC | 0.8624 |
| QWK | 0.6830 |

## Model Complexity

- Total parameters: 2,422,597
- Stage 1 training time: 14.27 minutes
- Stage 2 training time: 13.11 minutes

## Results Files

- `mobilenetv2_metrics.csv` – final evaluation metrics
- `MobileNetV2_Final_Summary.csv` – final experiment summary
- `stage1_history.csv` – Stage 1 training history
- `stage2_history.csv` – Stage 2 training history
- `stage1_accuracy.png` – Stage 1 accuracy curve
- `stage1_loss.png` – Stage 1 loss curve
- `stage2_accuracy.png` – Stage 2 accuracy curve
- `stage2_loss.png` – Stage 2 loss curve
- `confusion_matrix.png` – confusion matrix
- `roc_curve.png` – ROC curves
- `misclassified_examples.png` – examples of incorrect predictions
