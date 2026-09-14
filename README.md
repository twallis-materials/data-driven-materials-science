# Data-Driven Materials Science

Computational materials science workflows for composition-based machine learning, model validation across materials composition space, and microstructure image analysis.

This repository focuses on a central question in materials informatics:

> How reliably can data-driven models learn materials behaviour from limited descriptors, and how does their performance change when they are evaluated outside familiar regions of the data space?

The analyses combine materials descriptors, supervised and unsupervised learning, dimensionality reduction, group-aware validation, and convolutional neural networks.

---

## Highlights

### Composition-based materials classification

A set of 118 elemental-fraction descriptors was generated from chemical compositions in the Matminer dielectric dataset and used to predict the `pot_ferroelectric` target.

Five classification approaches were compared using stratified cross-validation:

- Logistic Regression
- Support Vector Machine
- Random Forest
- Gradient Boosting
- Neural Network

The Random Forest produced the strongest performance:

| Metric | Cross-validated score |
|---|---:|
| ROC-AUC | **0.934 ± 0.016** |
| Accuracy | **0.868 ± 0.020** |
| F1 | **0.904 ± 0.014** |
| Precision | **0.888 ± 0.021** |
| Recall | **0.921 ± 0.023** |

Feature analysis identified several composition descriptors that contribute strongly to the predictions. K was the highest-ranked descriptor under both random-forest and permutation importance, while Rb, Cs, Li, N, O, P, and Cu also appeared among influential features.

These rankings represent predictive associations within the dataset rather than direct physical mechanisms.

---

### Generalization across composition space

Strong performance under random cross-validation does not necessarily imply equally strong predictions in less familiar chemical regions.

To examine this, the composition descriptors were projected into a PCA representation and partitioned for group-aware validation.

Exploratory clustering showed weak separation and low stability, indicating that the dataset is better described as a heterogeneous, largely continuous composition space than as a small number of well-defined material classes.

The resulting partitions were therefore used as a stress test rather than interpreted as physical material families.

| Metric | Stratified CV | Group-aware CV |
|---|---:|---:|
| ROC-AUC | **0.934 ± 0.016** | **0.855 ± 0.093** |
| Accuracy | **0.868 ± 0.020** | **0.726 ± 0.070** |
| F1 | **0.904 ± 0.014** | **0.808 ± 0.040** |

The reduction in performance shows that prediction becomes more difficult when complete regions of composition space are withheld from training.

This distinction between interpolation and extrapolation is particularly important when evaluating machine-learning models for materials discovery.

---

### SEM microstructure classification

A convolutional neural network was used to distinguish local texture patterns in three SEM images.

Rather than relying only on a random patch split, the analysis also separates training and test patches spatially within each parent image.

| Validation strategy | Accuracy | Macro F1 |
|---|---:|---:|
| Random patch split | 0.973 | 0.973 |
| Spatial holdout | **0.946** | **0.946** |

The reduction under spatial holdout illustrates how validation strategy affects apparent image-classification performance.

Because only one parent image is available for each class, these results demonstrate discrimination of local texture within the available images and should not be interpreted as performance on independent specimens.

The source SEM images are not distributed with this repository because redistribution rights have not been established.

---

## Repository Structure

```text
data-driven-materials-science/
├── README.md
├── requirements.txt
├── .gitignore
│
├── notebooks/
│   ├── 01_data_selection_and_preprocessing.ipynb
│   ├── 02_ferroelectric_classification.ipynb
│   ├── 03_composition_space_analysis.ipynb
│   └── 04_sem_microstructure_classification.ipynb
│
├── data/
   ├── dielectric_composition_features.csv
   └── sem/
       └── README.md
```

---

## Analysis Workflow

### 01 — Data Selection and Preprocessing

[`01_data_selection_and_preprocessing.ipynb`](notebooks/01_data_selection_and_preprocessing.ipynb)

The Matminer dielectric dataset is converted into a reproducible composition-based representation.

The workflow:

- selects the target and relevant metadata;
- converts chemical formulas into composition objects;
- generates elemental-fraction descriptors;
- checks missing values and descriptor consistency;
- identifies zero-variance features;
- exports the processed dataset for downstream modelling.

The processed dataset contains:

- **1,056 materials**
- **118 elemental-fraction descriptors**
- **55 zero-variance descriptors identified**
- positive target fraction of approximately **0.671**

Feature removal is deferred to the machine-learning pipeline so that preprocessing can be handled consistently during model validation.

---

### 02 — Ferroelectric Classification

[`02_ferroelectric_classification.ipynb`](notebooks/02_ferroelectric_classification.ipynb)

This notebook compares several classification algorithms using the same composition representation and stratified cross-validation.

The analysis includes:

- preprocessing within ML pipelines;
- Logistic Regression;
- Support Vector Machine;
- Random Forest;
- Gradient Boosting;
- multilayer neural network;
- ROC-AUC, F1, precision, recall, and accuracy;
- random-forest hyperparameter search;
- feature-importance analysis;
- permutation importance.

Additional random-forest tuning did not improve upon the baseline model, indicating that the strong baseline result was not dependent on finding a narrowly optimized parameter configuration.

---

### 03 — Generalization Across Materials Composition Space

[`03_composition_space_generalization.ipynb`](notebooks/03_composition_space_generalization.ipynb)

This analysis investigates whether predictive performance changes when chemically separated regions of the dataset are withheld.

The workflow combines:

- zero-variance filtering;
- feature standardization;
- principal-component analysis;
- exploratory composition-space grouping;
- cluster-quality and stability diagnostics;
- leave-one-group-out validation;
- comparison with ordinary stratified cross-validation.

The exploratory groups show weak intrinsic separation and are therefore not interpreted as physical materials classes. Instead, they provide a reproducible partition for testing model sensitivity to changes in the represented composition domain.

---

### 04 — SEM Microstructure Classification

[`04_sem_microstructure_classification.ipynb`](notebooks/04_sem_microstructure_classification.ipynb)

This notebook applies a convolutional neural network to local SEM texture classification.

The workflow includes:

- grayscale image preprocessing;
- patch extraction;
- spatial train/test separation;
- CNN training;
- class-wise evaluation;
- comparison between random-patch and spatial-holdout validation.

The SEM source images are intentionally excluded from the public repository. The notebook focuses on the image-processing methodology and model evaluation without redistributing the original microscopy data.

---

## Methods

The repository uses a combination of:

**Materials informatics**
- composition-based descriptors
- elemental-fraction featurization
- Matminer datasets

**Machine learning**
- Logistic Regression
- Support Vector Machines
- Random Forests
- Gradient Boosting
- multilayer neural networks
- convolutional neural networks

**Model validation**
- stratified cross-validation
- group-aware validation
- leave-one-group-out testing
- hyperparameter search
- permutation importance

**Data analysis**
- principal-component analysis
- composition-space clustering
- cluster stability analysis
- scientific visualization

---

## Scientific Perspective

Materials datasets often contain strong correlations between chemistry, structure, processing history, and measured properties. High predictive performance alone therefore does not establish that a model has learned a transferable materials relationship.

The analyses in this repository place particular emphasis on validation strategy, domain coverage, and the distinction between interpolation and extrapolation.

The composition-based models intentionally exclude crystal structure, symmetry, defects, processing conditions, and temperature. Their predictions should therefore be interpreted within the information content of the selected descriptors.

---

## Tools

- Python
- NumPy
- pandas
- Matplotlib
- scikit-learn
- Matminer
- TensorFlow / Keras
- Jupyter

---

## Current Development

The next stage of this work extends the same materials-informatics framework toward sequential materials discovery, including:

- uncertainty-aware model selection;
- active learning;
- Bayesian optimization;
- exploration–exploitation strategies;
- closed-loop candidate selection.

The objective is to connect predictive materials modelling with workflows relevant to high-throughput and autonomous materials discovery.

---

## Author

**Theophilus Wallis, PhD**  
Computational Materials Scientist  
Berlin, Germany

Research interests include multiscale materials modelling, phase-field methods, CALPHAD-informed modelling, materials informatics, and AI/ML for materials discovery.
