# LoveHeaven at MAHED 2025: Text-based Hate and Hope Speech Classification

[![MAHED 2025](https://img.shields.io/badge/MAHED%202025-Sub--task%201-blue)](https://mahed.org/) [![Rank](https://img.shields.io/badge/Rank-4th-brightgreen)](#)

Welcome to the official repository for the **LoveHeaven** team's submission to the **MAHED 2025 Shared Task 1**: *Text-based Hate and Hope Speech Classification*.

Our system achieved **4th place** on the final leaderboard. This repository provides the complete source code and instructions to reproduce our results.

---

## 📜 System Overview

Our approach is a robust pipeline built upon the `bert-base-arabertv02-twitter` model. The overall workflow consists of the following key stages:

1.  **Data Processing**:
    * **Duplicate Handling**: We identified and handled approximately 320 duplicate entries in the training set to ensure data quality. Entries with the same text but conflicting labels were removed, while identical entries (text and label) were deduplicated to a single instance.
    * **Text Preprocessing**: We utilized the specialized `ArabertPreprocessor` to normalize text, remove non-Arabic characters, URLs, and @mentions.

2.  **Hyperparameter Tuning**:
    * We employed the **Optuna** framework combined with **Stratified K-Fold Cross-Validation** to automatically search for the optimal set of hyperparameters that maximized the Macro F1-score.

3.  **Ensemble Training and Prediction**:
    * After finding the best hyperparameters, we trained an **ensemble of 4 separate AraBERT-twitter models**. Each model was trained on a different data fold.
    * The final prediction is derived by **averaging the logits** from all 4 models, enhancing the system's robustness and stability.



---

## 🏆 Results

Our system achieved a final **Macro F1-score of 0.703** on the test set, securing 4th place on the official leaderboard. The `AraBERT-Twitter` model demonstrated superior performance compared to the base `AraBERT` model on both the validation and test datasets, confirming its suitability for social media text.

---

## 🚀 How to Reproduce

Please follow the steps below to reproduce our results.

### Environment and Dependencies

The system was developed and tested on **Kaggle Notebooks (free tier)** with the following configuration[cite: 65]:
* **GPU**: 1x NVIDIA Tesla P100 16GB 
* **RAM**: 13GB 
* **Python**: 3.11 
* **Key Libraries**:
    * `PyTorch 2.6.0` 
    * `Transformers 4.52.4` 
    * `Optuna 4.4.0` 

You can install all required dependencies by running:
```bash
pip install -r requirements.txt
