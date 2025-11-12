# Interactive-Multi-Label-CNN-Learning-with-Identity-Initialization


This project extends **Interactive Multi-Label CNN Learning with Partial Labels (CVPR 2020)**[link text]([CVPR 2020 Paper](https://openaccess.thecvf.com/content_CVPR_2020/html/Huynh_Interactive_Multi-Label_CNN_Learning_With_Partial_Labels_CVPR_2020_paper.html))
 by replacing the usual co-occurrence-based label graph prior with a simple **identity initialization**. The goal is to remove dataset-specific bias and let the model **learn label relationships from scratch**, improving robustness under partial/missing labels. 

---

## Overview

- **Problem:** Multi-label image classification with **incomplete labels** and **unknown label dependencies**.  
- **Key Idea:** Initialize the **label similarity graph = Identity matrix** instead of co-occurrence priors; refine it jointly with the CNN during training.   
- **Dataset:** **CUB-200-2011 (subset)** for fine-grained bird categories. 
- **Result (subset):** **mAP = 0.8214** on **18 valid classes**—competitive despite no co-occurrence prior. 

---

## Objectives

- Implement the interactive CNN + similarity-learner framework with **identity graph initialization**.   
- Train/evaluate on a **resource-constrained CUB subset** while preserving performance.   
- Measure multi-label performance via **mean Average Precision (mAP)**. 

---

## Methodology

### Data & Preprocessing
- Resize images to **224×224**, normalize with mean **[0.485, 0.456, 0.406]** and std **[0.229, 0.224, 0.225]**; convert to **RGB**.   
- One-hot labels; **80/20** train/test split; batch size **16** via PyTorch DataLoaders. 

### Identity Graph Initialization
- Build **G = Iₙ** (n = number of classes, here 200) so labels start **independent**; learn relations during training. 

### Training
- Multi-label classifier trained with **BCE + smoothness regularization** to encourage consistent predictions across similar labels/images.  
- Optimization with **SGD** and a dynamic learning rate schedule. 

### Evaluation
- Primary metric: **mAP** across classes; report observations and robustness under partial labels. 

---

## Results (CUB Subset)

- **Valid classes evaluated:** **18**  
- **Test mAP:** **0.8214**  
- **Takeaways:** Identity init + interactive learning maintains strong performance, **removing bias** from co-occurrence priors and remaining effective under limited compute/data. 

