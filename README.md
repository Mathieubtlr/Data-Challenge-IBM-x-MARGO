# hERG Inhibition Prediction Challenge (Télécom Paris, 2025)

![Python](https://img.shields.io/badge/Python-3.10%2B-blue)
![License](https://img.shields.io/badge/License-CC%20BY%204.0-green)
![Status](https://img.shields.io/badge/Competition-Finalist%20Top%205-yellow)

---

## 🔗 Summary

- [Overview](#-overview)  
- [Provided Datasets](#-provided-datasets)  
- [Copyright and License](#-copyright-and-license)  
- [Our Approach](#-our-approach)  
- [Random Forest Configuration](#-random-forest-configuration)  
- [Results](#-results)  
- [Visualizations](#-visualizations)  
- [Random Forest Tree (PDF)](arbre_random_forest_top.pdf)  
- [Training Notebook](training.ipynb)  
- [Dataset](train.csv)  
- [Test Set 1](test_1.csv)  
- [Test Set 2](test_2.csv)  
- [License (CC BY 4.0)](http://creativecommons.org/licenses/by/4.0/)

---

## Overview

This repository contains our solution to the **hERG Inhibition Prediction Hackathon**, organized at **Télécom Paris** by **MARGO**, **Qubit Pharmaceuticals**, and **IBM**, from **May 23–25, 2025**.

The goal of the hackathon was to develop a **binary classifier** capable of predicting whether a molecule is **toxic** or **non-toxic**.  
The toxicity studied is **hERG inhibition**, a major cause of cardiac side effects in certain drugs.

Our team proudly reached the **final stage (Top 5 out of 30 teams)** of the competition.

---

## Provided Datasets

Three datasets were provided in **CSV format**:

### Training Set (`train.csv`)
- **9415 molecules**  
- 1 `smiles` column: canonical SMILES representation of each molecule  
- **199** molecular features computed with the **RDKit** package  
- **2048** columns (`ecfc_XXXX`): bit vector representation of **Morgan fingerprints**  
- **2048** columns (`fcfc_XXXX`): bit vector representation of **pharmacophore feature-based Morgan fingerprints**  
- 1 `class` column: target label (`1` = hERG inhibitor, `0` = non-inhibitor)

Note : We didn't pushed the database because it exceeds 100 Mo. 

### Test Set 1 (`test_1.csv`)
- **750 molecules**
- Same structure as the training dataset, **without** the `class` label

### Test Set 2 (`test_2.csv`)
- **478 molecules**
- 1 `series` column identifying the molecular series of each compound  
- Same set of features and fingerprints as in the training data

All molecular features and fingerprints were generated using the  
**RDKit Python package (version 2023.03.1)** — https://www.rdkit.org/

---

## Copyright and License

Datasets used in this event were derived from the following open-access research article:

> Karim, A., Lee, M., Balle, T. *et al.*  
> **CardioTox net: a robust predictor for hERG channel blockade based on deep learning meta-feature ensembles.**  
> *Journal of Cheminformatics* 13, 60 (2021).  
> [https://doi.org/10.1186/s13321-021-00541-z](https://doi.org/10.1186/s13321-021-00541-z)

Molecules were preprocessed by **Qubit Pharmaceuticals**, and all features were generated with **RDKit**.

**License:**  
Open Access — This dataset is licensed under the  
[Creative Commons Attribution 4.0 International License (CC BY 4.0)](http://creativecommons.org/licenses/by/4.0/).

---

## Our Approach

Our approach focused on designing a **robust, interpretable machine learning pipeline** using classical algorithms (Random Forests and Gradient Boosting) with optimized molecular descriptors.

### Steps
1. **Data preprocessing**
   - Missing value handling  
   - Feature standardization and correlation filtering  

2. **Feature engineering**
   - RDKit-based molecular descriptors  
   - Morgan and pharmacophore fingerprints  

3. **Modeling**
   - Main model: **Random Forest Classifier**  
   - Benchmarks: Gradient Boosting, Logistic Regression  
   - Hyperparameter tuning via Grid Search  

4. **Evaluation**
   - Cross-validation on training set  
   - Metrics: ROC-AUC, accuracy, precision, recall  

---

## Random Forest Configuration

| Parameter | Value |
|:-----------|:------|
| Number of estimators | 500 |
| Max depth | Tuned (5–25) |
| Criterion | Gini |
| Bootstrap | True |
| Random state | 42 |

Feature selection was performed with **Recursive Feature Elimination (RFE)**.  
A visualization of one of the top-performing trees is available in:  
`arbre_random_forest_top.pdf`

The main program is in **classification algorithm** -> **training.ipynb**

---

## Results

| Metric | Validation Score |
|:--------|:----------------:|
| ROC-AUC | **0.93** |
| Accuracy | **0.88** |
| Precision | **0.85** |
| Recall | **0.81** |

Our final model achieved a **Top 5 ranking** among 30 participating teams.

---

## Authors

**Institution:** Télécom Paris  
**Members:** PELISSIER Etienne, PREVOST Antoine, NGHIEM Bérénice, BOUTEILLER Mathieu   
**Achievement:** Finalist – **Top 5 out of 30 Teams**

---

