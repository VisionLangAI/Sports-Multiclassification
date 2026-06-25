# SportNeXt-ViT: Sports Image Classification

This repository provides implementation details for the SportNeXt-ViT framework, a hybrid deep learning model for image-based sports type classification. The framework integrates ConvNeXt for local feature extraction and Vision Transformer (ViT) for global contextual representation, followed by a bi-directional cross-attention fusion module.

## Task

The task is multi-class sports image classification using a publicly available Kaggle sports image dataset. The model classifies still images into 22 sports categories.

## Dataset

The dataset is publicly available from Kaggle:

`https://www.kaggle.com/datasets/rishikeshkonapure/sports-image-dataset`

The dataset contains 22 sports classes with approximately 13,624 images. The data were divided using a fixed random seed to ensure reproducibility.

## Experimental Split

A stratified split was used to preserve class distribution across partitions. The test set was kept completely unseen during training and validation. Data augmentation was applied only after splitting and only to the training images.

## Preprocessing and Augmentation

All images were resized to `224 × 224` pixels. The augmentation pipeline included:

- Random horizontal flip
- Random rotation
- Color jittering
- Gaussian noise
- Normalization

Validation and test images were not augmented.

## Implementation Details

The experiments were conducted using:

- Python 3.11
- PyTorch 2.2
- CUDA 12.1
- NVIDIA RTX 4090 GPU
- Image size: 224 × 224
- Batch size: 32
- Optimizer: AdamW
- Weight decay: 1e-4
- Training epochs: 100
- Early stopping patience: 10
- Random seed: 42
- Learning-rate scheduler: Cosine annealing

## Model Architecture

SportNeXt-ViT consists of three main components:

1. **ConvNeXt branch** for fine-grained local spatial feature extraction.
2. **Vision Transformer branch** for global contextual representation.
3. **Bi-directional cross-attention fusion module** for adaptive local-global feature interaction.

The ViT backbone uses 12 self-attention heads, while the proposed cross-attention fusion module uses 4 attention heads.

## Evaluation Metrics

The model was evaluated using:

- Accuracy
- Macro precision
- Macro recall
- Macro F1-score
- Weighted precision
- Weighted recall
- Weighted F1-score
- Macro one-vs-rest AUC

All metrics are reported in percentage format.

## Explainability

Qualitative explainability was performed using:

- Grad-CAM
- LIME
- SHAP

These methods provide qualitative plausibility evidence for model predictions. Quantitative XAI faithfulness checks such as insertion-deletion and randomization tests are recommended for future work.

## Reproducibility Notes

To reproduce the experiments, use the same random seed, stratified split protocol, preprocessing pipeline, model configuration, and training settings described above. Raw prediction files, split indices, and additional implementation details may be provided as supplementary material or upon reasonable request.

## Citation

If this work is used, please cite the associated manuscript:

`A Novel Model based on Fusion of Cross-Attention ConvNeXt and Vision Transformers for Automated Classification of Sport Types`
