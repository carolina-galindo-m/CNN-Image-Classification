# 🧠 CNN Image Classification — Hyperparameter Tuning & Data Augmentation

**Course:** Advanced Machine Learning  
**Assignment:** A1 — Neurals  
**Student:** Carolina Galindo Mendoza  
**Institution:** Hult International Business School  
**Professor:** Anusha Vissapragada  
**Date:** March 15, 2026  

---

## 📌 Project Overview

This project explores how **hyperparameter tuning and data augmentation** impact the performance of a **Convolutional Neural Network (CNN)** for image classification. The model is trained on a **cats-only subset** of the Oxford-IIIT Pet Dataset, focusing on identifying **12 cat breeds**.

The objectives of this project are to:
- Design and implement a custom CNN architecture
- Systematically evaluate the effect of key hyperparameters
- Reduce overfitting on a small dataset using data augmentation
- Compare configurations from both **technical and business perspectives**

---

## 📂 Dataset Setup — Cats Only

- **Dataset:** Oxford-IIIT Pet Dataset  
- **Subset:** 12 cat breeds  
- **Approximate size:** ~3,000 images (~250 per class)

### Cat Breeds Included
- Abyssinian  
- Bengal  
- Birman  
- Bombay  
- British Shorthair  
- Egyptian Mau  
- Maine Coon  
- Persian  
- Ragdoll  
- Russian Blue  
- Siamese  
- Sphynx  

### Preprocessing
- Resize images to **128×128**
- Convert images to PyTorch tensors
- Normalize using ImageNet mean and standard deviation
- Remap original dataset labels to a **0–11 class index**

---

## 🧩 CNN Architecture

A lightweight CNN was intentionally chosen to keep experiments interpretable and computationally efficient.

### Architecture Components

**Feature Extractor**
- 3 convolutional blocks  
- Each block: `Conv2D → ReLU → MaxPool`
- Channel progression: **32 → 64 → 128**

**Pooling**
- Adaptive Average Pooling to `(1,1)`

**Classifier**
- Fully connected layer: `128 → 256`
- ReLU activation
- Dropout (configurable)
- Output layer: 12 classes

This architecture balances model capacity and generalization on a small dataset.

---

## ⚙️ Training Pipeline

The training pipeline includes:
- Automatic CPU/GPU detection
- Adam optimizer
- Cross-entropy loss
- Accuracy tracking per epoch
- Modular training function returning loss and accuracy history
- Model saving to Google Drive

Additional pipeline elements:
- Input scaling
- Feature engineering
- Feature selection
- Hyperparameter-controlled experimentation loop

---

## 🧪 Hyperparameter Configurations

Four configurations were designed to isolate the impact of individual hyperparameters.

| Config | Learning Rate | Epochs | Batch Size | Dropout | Augmentation | Notes |
|------|--------------|--------|------------|---------|--------------|------|
| 1 — Baseline | 1e-3 | 10 | 32 | 0.3 | No | Starter defaults |
| 2 — Lower LR | 1e-4 | 10 | 32 | 0.3 | No | Slower learning |
| 3 — High Dropout | 1e-3 | 10 | 64 | 0.5 | No | Strong regularization |
| 4 — Best Model | 5e-4 | 15 | 32 | 0.4 | ✅ Yes | Tuned + augmented |

Each setup modifies **one or two variables** to clearly observe their effects.

---

## 🔄 Data Augmentation (Final Model)

To reduce overfitting on a small dataset, data augmentation was applied in the final configuration:

- Random resized crops (128×128)
- Random horizontal flips
- Random rotations (±15°)
- Color jitter (brightness, contrast, saturation, hue)
- Normalization using ImageNet statistics

Data augmentation expands the effective training distribution with **no inference-time cost**.

---

## 📊 Results Comparison

| Configuration | Final Accuracy |
|---------------|---------------|
| Baseline (Config 1) | 16.8% |
| Lower LR (Config 2) | 12.9% |
| High Dropout (Config 3) | 15.7% |
| ✅ Best Model (Config 4) | **21.9%** |

**Performance Gain**
- Absolute improvement: **+5.1 percentage points**
- Relative improvement: **~30% over baseline**

Training loss and accuracy curves are generated and saved for all configurations.

---

## ✅ Key Findings

- A learning rate of **5e-4** balanced stability and convergence speed.
- **Dropout = 0.4** offered effective regularization without excessive capacity loss.
- Increasing epochs improved performance only when paired with appropriate learning rates.
- **Data augmentation was the most impactful improvement**, surpassing tuning alone.
- Aggressive regularization and larger batch sizes hurt performance on small datasets.

---

## 🧠 Business Perspective

- The **baseline model** offers the best accuracy-per-compute ratio.
- The **best model** achieves higher accuracy but requires ~50% more compute.
- Whether a 5-point accuracy gain is worth the cost depends on use case.
- All models remain **far below production-ready performance**.

**Key takeaway:** Model performance is limited more by architecture and dataset size than by hyperparameter choices.

**Recommended next step:** Transfer learning using a pretrained CNN backbone.

---

## 📦 Final Deliverables Summary

- ✅ Custom CNN architecture  
- ✅ Four controlled hyperparameter experiments  
- ✅ Augmented best-performing model  
- ✅ Training curves and comparison tables  
- ✅ Technical and business interpretation  

---

## 📌 Final Model Configuration

- **Option:** Cats Only (12 Classes)  
- **Learning Rate:** 5e-4  
- **Epochs:** 15  
- **Batch Size:** 32  
- **Dropout:** 0.4  
- **Data Augmentation:** Yes  
- **Final Training Accuracy:** 21.9%  

---
