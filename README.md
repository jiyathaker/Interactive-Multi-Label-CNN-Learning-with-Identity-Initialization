# Interactive-Multi-Label-CNN-Learning-with-Identity-Initialization
# Interactive Multi-Label CNN Learning with Identity Initialization

**Course:** CS 715 — Advanced Data Science & Machine Learning  
**Instructor:** Dr. JingTao Yao  
**Author:** Jiya Thaker (200511800)  
**Term:** December 2024

This project extends **Interactive Multi-Label CNN Learning with Partial Labels (CVPR 2020)** by replacing the usual co-occurrence-based label graph prior with a simple **identity initialization**. The goal is to remove dataset-specific bias and let the model **learn label relationships from scratch**, improving robustness under partial/missing labels. :contentReference[oaicite:0]{index=0}

---

## Overview

- **Problem:** Multi-label image classification with **incomplete labels** and **unknown label dependencies**.  
- **Key Idea:** Initialize the **label similarity graph = Identity matrix** instead of co-occurrence priors; refine it jointly with the CNN during training. :contentReference[oaicite:1]{index=1}  
- **Dataset:** **CUB-200-2011 (subset)** for fine-grained bird categories. :contentReference[oaicite:2]{index=2}  
- **Result (subset):** **mAP = 0.8214** on **18 valid classes**—competitive despite no co-occurrence prior. :contentReference[oaicite:3]{index=3}

---

## Objectives

- Implement the interactive CNN + similarity-learner framework with **identity graph initialization**. :contentReference[oaicite:4]{index=4}  
- Train/evaluate on a **resource-constrained CUB subset** while preserving performance. :contentReference[oaicite:5]{index=5}  
- Measure multi-label performance via **mean Average Precision (mAP)**. :contentReference[oaicite:6]{index=6}

---

## Methodology

### Data & Preprocessing
- Resize images to **224×224**, normalize with mean **[0.485, 0.456, 0.406]** and std **[0.229, 0.224, 0.225]**; convert to **RGB**. :contentReference[oaicite:7]{index=7}  
- One-hot labels; **80/20** train/test split; batch size **16** via PyTorch DataLoaders. :contentReference[oaicite:8]{index=8}

### Identity Graph Initialization
- Build **G = Iₙ** (n = number of classes, here 200) so labels start **independent**; learn relations during training. :contentReference[oaicite:9]{index=9}

### Training
- Multi-label classifier trained with **BCE + smoothness regularization** to encourage consistent predictions across similar labels/images.  
- Optimization with **SGD** and a dynamic learning rate schedule. :contentReference[oaicite:10]{index=10}

### Evaluation
- Primary metric: **mAP** across classes; report observations and robustness under partial labels. :contentReference[oaicite:11]{index=11}

---

## Results (CUB Subset)

- **Valid classes evaluated:** **18**  
- **Test mAP:** **0.8214**  
- **Takeaways:** Identity init + interactive learning maintains strong performance, **removing bias** from co-occurrence priors and remaining effective under limited compute/data. :contentReference[oaicite:12]{index=12}


