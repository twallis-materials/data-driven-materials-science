# Data-Driven Materials Science

Machine learning and data-driven workflows for materials prediction, composition-space analysis, and microstructure classification.

## Overview

This repository contains a collection of materials-informatics studies exploring how chemical composition and microstructural information can be used to classify, organize, and interpret materials data.

The projects originated from my training in **Data-Driven Materials Science at the Interdisciplinary Centre for Advanced Materials Simulation (ICAMS), Ruhr University Bochum**, and are being reorganized and updated as reproducible materials-informatics case studies.

The repository covers two main case studies:

1. **Composition-Based Materials Informatics** — an end-to-end workflow covering dataset selection, preprocessing, supervised machine learning, unsupervised learning, and model validation.
2. **Deep Learning for Materials Characterization** — a computer-vision study using convolutional neural networks to classify scanning electron microscopy (SEM) images.

The broader objective is to explore how data-driven methods can complement physics-based materials modelling and contribute to materials discovery, characterization, and optimization.

---

## Case Study I — Composition-Based Materials Informatics

This case study develops an end-to-end machine-learning workflow for composition-based materials analysis, beginning with raw materials data and progressing to predictive modelling, composition-space exploration, and model validation.

The workflow is organized into three stages:

**Data Selection & Preprocessing → Supervised Learning → Composition-Space Analysis & Extrapolative Validation**

### 1. Data Selection and Preprocessing

The first stage establishes the materials dataset used throughout the composition-based studies.

The workflow includes:

- selection of a materials dataset
- data cleaning and preprocessing
- processing of chemical formulas
- construction of composition-based features
- preparation of target properties for machine learning
- identification and treatment of unsuitable or constant features
- generation of a consistent dataset for downstream analysis

The processed dataset produced at this stage provides the input for both the supervised and unsupervised machine-learning studies.

This step is treated as an integral part of the materials-informatics workflow because the reliability and physical meaning of subsequent machine-learning results depend strongly on data quality, feature construction, and target definition.

---

### 2. Composition-Based Prediction of Ferroelectric Materials

The second stage investigates whether chemical composition can be used to identify materials with potential ferroelectric behaviour.

Multiple supervised machine-learning algorithms are compared, including:

- Logistic Regression
- Support Vector Machines
- Random Forests
- Gradient Boosting
- Neural Networks

Model evaluation includes:

- cross-validation
- accuracy
- precision
- recall
- F1-score
- ROC-AUC analysis
- hyperparameter optimization

The study examines the predictive information contained in chemical composition while recognizing an important materials-science limitation: ferroelectric behaviour is not determined by composition alone.

Crystal structure, symmetry, phase stability, temperature, defects, processing history, and other physical factors can also influence ferroelectric behaviour.

The project therefore provides both a machine-learning classification study and an example of the importance of physically informed interpretation of data-driven materials models.

---

### 3. Composition-Space Analysis and Unsupervised Learning

The third stage explores the structure of the materials dataset in chemical-composition space using unsupervised machine learning.

Methods investigated include:

- dimensionality reduction
- t-SNE visualization
- clustering
- DBSCAN
- composition-space grouping
- leave-one-group-out cross-validation
- comparison of random and group-based validation

A particular focus is the distinction between **interpolation and extrapolation** in materials machine learning.

Random cross-validation can place chemically similar materials in both the training and validation sets. This may provide an optimistic estimate of model performance when the ultimate objective is to predict materials in previously unexplored regions of composition space.

Group-based validation provides an alternative way of examining how predictive models perform when evaluated on compositionally distinct groups of materials.

The original study uses t-SNE and DBSCAN as exploratory tools for visualizing and identifying structure in composition space. In the updated workflow, these results are interpreted cautiously because distances and clusters in a low-dimensional t-SNE representation do not necessarily preserve the full geometry of the original high-dimensional composition space.

This project therefore emphasizes not only model performance, but also the broader problem of **generalization and extrapolation in data-driven materials discovery**.

---

## Case Study II — Deep Learning for Materials Characterization

### 4. SEM Microstructure Classification

This case study explores deep learning for the classification of scanning electron microscopy (SEM) images of metal-nitride thin films.

The workflow includes:

- SEM image preprocessing
- grayscale conversion
- image patch generation
- neural-network classification
- convolutional neural networks (CNNs)
- confusion-matrix analysis
- precision, recall, accuracy, and F1-score evaluation
- investigation of image-size effects on classification performance

The project demonstrates how computer-vision methods can extract microstructural information directly from experimental materials images.

The current study is treated as a **proof-of-concept microstructure classification problem**.

Because image patches can originate from the same parent SEM micrograph, random patch-level train/test splitting may lead to optimistic estimates of model generalization. A more rigorous assessment of transferability would require validation using independent micrographs or specimens.

This limitation is explicitly considered as part of the scientific interpretation of the deep-learning results.

---

## Repository Structure

```text
data-driven-materials-science/
│
├── README.md
├── requirements.txt
│
├── notebooks/
│   ├── 01_data_selection_and_preprocessing.ipynb
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
```

---

## Machine-Learning Methods

The repository covers several areas of machine learning and data analysis:

### Supervised Learning

- Logistic Regression
- Support Vector Machines
- Random Forests
- Gradient Boosting
- Neural Networks

### Unsupervised Learning

- Dimensionality Reduction
- t-SNE
- DBSCAN
- Clustering
- Composition-Space Exploration

### Deep Learning

- Artificial Neural Networks
- Convolutional Neural Networks
- Image Classification

### Model Evaluation

- Cross-Validation
- Leave-One-Group-Out Validation
- Accuracy
- Precision
- Recall
- F1-score
- ROC-AUC
- Confusion Matrices
- Hyperparameter Optimization

---

## Computational Tools

The projects are primarily implemented in Python using scientific-computing and machine-learning tools including:

- Python
- NumPy
- pandas
- Matplotlib
- scikit-learn
- TensorFlow / Keras
- Matminer

---

## Scientific Perspective

Machine learning in materials science is most valuable when combined with physical understanding.

My broader research background is in computational materials science, including:

- materials thermodynamics and kinetics
- phase-field modelling
- CALPHAD
- atomistic simulations
- grain-boundary thermodynamics
- segregation and interfacial phase transformations
- multicomponent metallic systems
- liquid-metal embrittlement
- multiscale materials modelling

I am particularly interested in connecting physics-based materials modelling with data-driven approaches.

The long-term objective is to combine:

**Physics-Based Modelling + Materials Informatics + Machine Learning + Materials Design**

to accelerate the understanding, discovery, and optimization of materials for energy, structural, and sustainable engineering applications.

---

## Current Development

These projects originated from earlier Data-Driven Materials Science studies and are currently being reorganized and modernized for reproducibility and clearer scientific interpretation.

Planned improvements include:

- modernized scikit-learn workflows
- reproducible preprocessing pipelines
- improved cross-validation strategies
- feature-importance analysis
- explainable machine learning
- physically informed feature engineering
- improved extrapolative validation
- clearer uncertainty and limitation analysis

Future extensions will explore:

- active learning
- Bayesian optimization
- multi-objective materials optimization
- autonomous materials discovery workflows

---

## Author

**Theophilus Wallis, PhD**

Computational Materials Scientist  
Berlin, Germany

Research interests: computational materials science, multiscale materials modelling, materials thermodynamics, phase-field modelling, CALPHAD, atomistic simulation, materials informatics, and machine learning for materials research.
