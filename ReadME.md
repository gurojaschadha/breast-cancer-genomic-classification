# Multi-Modal Transcriptomic Classification of Breast Cancer

This repository contains the code, models, and evaluation framework for the research paper: **[Insert Your Chosen Title Here]**.

## Overview
Accurate molecular subtyping of breast cancer is paramount for targeted oncology, yet transcriptomic classification is severely bottlenecked by the "curse of dimensionality" ($p \gg n$). This project evaluates the diagnostic efficacy of traditional ensemble learning, deep tabular architectures, and Large Language Models (LLMs) on high-dimensional genomic data.

The methodology addresses severe class imbalance and extreme dimensionality (54,675 gene probes) through variance-based filtration, Z-score standardization, and semantic serialization, ultimately comparing numerical deep learning against NLP-based prompt classification.

## Dataset
The study utilizes the **CuMiDa (Curated Microarray Database)** Breast Cancer dataset (GSE45827).
* **Initial Feature Space:** 54,675 genes across 151 patient samples.
* **Classes:** 6 molecular subtypes (Basal, Luminal A, Luminal B, HER2, Cell Line, Normal).
* *Note: Due to size constraints, the raw dataset is not hosted in this repository. It can be downloaded directly from the [CuMiDa repository](https://sbcb.inf.ufrgs.br/cumida).*

## Model Architectures
1. **XGBoost (Baseline):** Regularized gradient boosting with histogram-based tree construction and random column sampling.
2. **TabNet:** A deep tabular architecture utilizing sequential attention mechanisms and sparsity regularization to isolate critical biomarkers.
3. **Genomic ResNet (GRN):** A custom 1D Residual Network featuring skip connections to prevent gradient vanishing on small sample sizes.
4. **Denoising Autoencoder (DAE):** A self-supervised framework that compresses 10,000 noisy genes into a 128-dimensional latent space prior to classification.
5. **DistilBERT (LLM):** A generative language model fine-tuned on stochastically augmented, semantically serialized text prompts representing top-variance genes.

## Results
Empirical evaluation identified **TabNet** and the **Denoising Autoencoder** as the most effective diagnostic frameworks, efficiently attenuating biological noise and mitigating information leakage between closely related subtypes.

| Model Architecture | Accuracy | Precision (Macro) | Recall (Macro) | F1 (Macro) | F1 (Weighted) |
| :--- | :---: | :---: | :---: | :---: | :---: |
| XGBoost (Baseline) | 0.9032 | 0.92 | 0.86 | 0.88 | 0.90 |
| Genomic ResNet (GRN) | 0.9032 | 0.93 | 0.86 | 0.88 | 0.90 |
| DistilBERT (LLM) | 0.7419 | 0.77 | 0.77 | 0.74 | 0.74 |
| Denoising Autoencoder (DAE) | **0.9677** | **0.98** | 0.97 | 0.97 | **0.97** |
| TabNet (Deep Tabular) | **0.9677** | **0.98** | **0.98** | **0.98** | **0.97** |

## Repository Structure
* `/notebooks/` - Contains the Jupyter/Colab notebooks for model training and evaluation.
  * `01_XGBoost_Baseline.ipynb`
  * `02_TabNet_Classification.ipynb`
  * `03_Custom_ResNet_and_DAE.ipynb`
  * `04_DistilBERT_LLM_Serialization.ipynb`
* `/utils/` - Helper scripts for data preprocessing and metric generation.
* `requirements.txt` - Python dependencies.

