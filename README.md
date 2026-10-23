# Groundnut Leaf Disease Detection

A deep learning-based image classification system for detecting diseases and health conditions in groundnut leaves using EfficientNet-B0 and transfer learning.

The model classifies groundnut leaf images into five categories:

- Early Leaf Spot
- Late Leaf Spot
- Rust
- Nutrition Deficiency
- Healthy

## Project Overview

Groundnut is widely cultivated in rain-fed regions of South India. Leaf diseases can significantly affect crop health and yield if they are not identified at an early stage.

This project develops an automated groundnut leaf disease classifier using computer vision and deep learning. Since the dataset contains class imbalance, class-weighted training is used and Macro F1-score is considered the primary evaluation metric.

## Dataset

Dataset: Dataset of Groundnut Plant Leaf Images  
Source: Mendeley Data  
Link: https://data.mendeley.com/datasets/22p2vcbxfk/3

The dataset folders were mapped into five target classes required for the classification task.

| Class | Label |
|---|---:|
| Early Leaf Spot | 0 |
| Late Leaf Spot | 1 |
| Rust | 2 |
| Nutrition Deficiency | 3 |
| Healthy | 4 |

The early_rust_1 and rust_1 folders were mapped to the common Rust target class.

### Dataset Split

| Dataset | Number of Images |
|---|---:|
| Training | 6,328 |
| Validation | 1,582 |
| Testing | 2,451 |
| Total | 10,361 |

The provided test set was kept separate for final evaluation. The training data was further divided into training and validation sets using stratified splitting.

## Preprocessing

All images are resized to 224 × 224 pixels before being passed to the model.

ImageNet normalization is applied using:

```text
Mean = [0.485, 0.456, 0.406]
Std  = [0.229, 0.224, 0.225]
```

Training-time augmentation includes:

- Random horizontal flipping
- Random rotation
- Brightness adjustment
- Contrast adjustment

Random augmentation is applied only to the training dataset.

## Model

The project uses EfficientNet-B0 with transfer learning.

A pretrained ImageNet EfficientNet-B0 model is loaded and its final classification layer is replaced with a five-class output layer.

### Training Configuration

| Parameter | Value |
|---|---|
| Architecture | EfficientNet-B0 |
| Transfer Learning | ImageNet pretrained |
| Input Size | 224 × 224 |
| Number of Classes | 5 |
| Optimizer | AdamW |
| Learning Rate | 0.0001 |
| Batch Size | 32 |
| Epochs | 10 |
| Loss Function | Weighted Cross-Entropy |
| Primary Metric | Macro F1-score |

Class weights are calculated from the training distribution and supplied to the cross-entropy loss to reduce the effect of class imbalance.

The best model is selected according to validation Macro F1-score.

## Results

The final model was evaluated on 2,451 test images.

| Metric | Result |
|---|---:|
| Test Accuracy | 97.55% |
| Balanced Accuracy | 97.04% |
| Macro F1-score | 0.9705 |

### Per-Class Performance

| Class | F1-score |
|---|---:|
| Early Leaf Spot | 0.9292 |
| Late Leaf Spot | 0.9412 |
| Rust | 1.0000 |
| Nutrition Deficiency | 1.0000 |
| Healthy | 0.9820 |

Macro F1-score is used as the main evaluation metric because it gives equal importance to each class regardless of the number of images available for that class.

## Evaluation

The model is evaluated using:

- Accuracy
- Balanced Accuracy
- Macro F1-score
- Precision
- Recall
- Per-class F1-score
- Classification Report
- Confusion Matrix
- Random Test Predictions

Learning curves are also generated to compare training and validation performance across epochs.

## Sample Prediction

For an unseen leaf image, the trained model produces both the predicted class and its confidence score.

Example output:

```text
Prediction : Early Leaf Spot
Confidence : 98.42%
```

Random samples from the test dataset are also visualized with:

```text
Actual Class
Predicted Class
Confidence Score
Correct / Incorrect
```

This provides a clear qualitative view of the model's predictions in addition to the quantitative evaluation metrics.

## Project Workflow

```text
Groundnut Leaf Images
        |
        v
Dataset Preparation
        |
        v
5-Class Label Mapping
        |
        v
Train / Validation / Test
        |
        v
Image Preprocessing
        |
        v
Data Augmentation
        |
        v
Class-Weighted Training
        |
        v
EfficientNet-B0
        |
        v
Disease Classification
        |
        v
Macro F1 + Balanced Accuracy
        |
        v
Confusion Matrix + Predictions
```

## Technologies Used

- Python
- PyTorch
- Torchvision
- EfficientNet-B0
- Scikit-learn
- Pandas
- NumPy
- Matplotlib
- Pillow
- Google Colab

## Repository Contents

```text
Groundnut-Leaf-Disease-Detection/
│
├── groundnutleafdiseaseclassification.ipynb
├── README.md
├── report/
│   └── Groundnut_Leaf_Disease_Report.pdf
├── results/
│   ├── confusion_matrix.png
│   ├── learning_curves.png
│   └── sample_predictions.png
└── model/
    └── best_groundnut_model.pth
```

The exact repository structure can be adjusted depending on which result files and trained model files are uploaded.

## How to Run

1. Clone or download this repository.
2. Download the groundnut leaf dataset from Mendeley Data.
3. Upload the dataset to Google Colab or connect Google Drive.
4. Extract the dataset.
5. Update the dataset path if required.
6. Run the notebook cells sequentially.
7. Train the EfficientNet-B0 model.
8. Evaluate the best model on the test dataset.
9. Upload a new groundnut leaf image to obtain a disease prediction.

GPU acceleration is recommended for model training.

## Conclusion

The EfficientNet-B0 transfer-learning model achieved a test accuracy of 97.55% and a Macro F1-score of 0.9705 for five-class groundnut leaf classification.

The results demonstrate the potential of deep learning and computer vision for automated plant disease identification. Future improvements can include testing on more diverse real-field images, comparing additional architectures, improving disease localization, and deploying the trained model through a web or mobile application for practical agricultural use.

## License and Dataset Attribution

The groundnut leaf images used in this project originate from the Mendeley Data groundnut plant leaf image dataset. Users of this repository should follow the licensing and attribution requirements specified by the original dataset authors.

This repository is intended for educational and research purposes.
