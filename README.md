# Data-Driven Materials Science

Machine learning and data-driven workflows for materials prediction, composition-space analysis, and microstructure classification.

## Overview

This repository contains a collection of materials-informatics studies exploring how chemical composition and microstructural information can be used to classify, organize, and interpret materials data.

The projects originated from my training in **Data-Driven Materials Science at ICAMS, Ruhr University Bochum**, and have been reorganized as reproducible case studies with a focus on scientific interpretation, model validation, and materials-engineering relevance.

The repository covers three main themes:

1. **Composition-based materials classification**
2. **Materials-space exploration and extrapolative validation**
3. **Deep learning for SEM microstructure classification**

---

## Projects

### 1. Composition-Based Prediction of Ferroelectric Materials

This project investigates whether chemical composition alone can be used to identify materials with potential ferroelectric behaviour.

Methods include:

- composition-based feature generation
- data preprocessing
- logistic regression
- support vector machines
- random forests
- gradient boosting
- neural networks
- cross-validation
- ROC-AUC analysis
- hyperparameter optimization

A central question in this study is the extent to which composition-only models can capture materials behaviour that is also influenced by crystal structure, symmetry, phase stability, temperature, and defects.

---

### 2. Composition-Space Analysis and Unsupervised Learning

This project explores the structure of materials datasets in chemical-composition space.

Methods include:

- dimensionality reduction
- t-SNE visualization
- clustering
- DBSCAN
- leave-one-group-out cross-validation
- comparison of interpolation and extrapolation performance

The study is particularly focused on how predictive performance changes when a model is evaluated on compositionally distinct groups rather than randomly selected samples.

---

### 3. Deep Learning for SEM Microstructure Classification

This project explores convolutional neural networks for classification of scanning electron microscopy images of metal-nitride thin films.

Methods include:

- SEM image preprocessing
- grayscale conversion
- image patch generation
- neural networks
- convolutional neural networks
- confusion matrices
- precision, recall, accuracy, and F1-score analysis
- image-size sensitivity studies

This project is treated as a **proof-of-concept microstructure classification study**. Particular attention is given to the distinction between random patch-level validation and true generalization to independent specimens or micrographs.

---

## Repository Structure

```text
data-driven-materials-science/
│
├── README.md
├── requirements.txt
│
├── notebooks/
│   ├── 01_data_preprocessing.ipynb
│   ├── 02_ferroelectric_classification.ipynb
│   ├── 03_composition_space_analysis.ipynb
│   └── 04_sem_microstructure_classification.ipynb
│
├── src/
│   ├── preprocessing.py
│   ├── evaluation.py
│   └── visualization.py
│
├── data/
│   └── README.md
│
├── figures/
│
└── reports/
