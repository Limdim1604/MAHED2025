# LoveHeaven at MAHED 2025: Text-based Hate and Hope Speech Classification

[![MAHED 2025](https://img.shields.io/badge/MAHED%202025-Sub--task%201-blue)](https://mahed.org/) [![Rank](https://img.shields.io/badge/Rank-4th-brightgreen)](#)

[cite_start]Welcome to the official repository for the **LoveHeaven** team's submission to the **MAHED 2025 Shared Task 1**: *Text-based Hate and Hope Speech Classification*[cite: 4].

[cite_start]Our system achieved **4th place** on the final leaderboard[cite: 6, 90]. This repository provides the complete source code and instructions to reproduce our results.

---

## 📜 System Overview

[cite_start]Our approach is a robust pipeline built upon the `bert-base-arabertv02-twitter` model[cite: 5]. The overall workflow consists of the following key stages:

1.  **Data Processing**:
    * [cite_start]**Duplicate Handling**: We identified and handled approximately 320 duplicate entries in the training set to ensure data quality[cite: 48]. [cite_start]Entries with the same text but conflicting labels were removed, while identical entries (text and label) were deduplicated to a single instance[cite: 54, 55].
    * [cite_start]**Text Preprocessing**: We utilized the specialized `ArabertPreprocessor` to normalize text, remove non-Arabic characters, URLs, and @mentions[cite: 37, 39].

2.  **Hyperparameter Tuning**:
    * [cite_start]We employed the **Optuna** framework combined with **Stratified K-Fold Cross-Validation** to automatically search for the optimal set of hyperparameters that maximized the Macro F1-score[cite: 5].

3.  **Ensemble Training and Prediction**:
    * After finding the best hyperparameters, we trained an **ensemble of 4 separate AraBERT-twitter models**. [cite_start]Each model was trained on a different data fold[cite: 61].
    * [cite_start]The final prediction is derived by **averaging the logits** from all 4 models, enhancing the system's robustness and stability[cite: 62].



---

## 🏆 Results

[cite_start]Our system achieved a final **Macro F1-score of 0.703** on the test set, securing 4th place on the official leaderboard[cite: 84, 90]. [cite_start]The `AraBERT-Twitter` model demonstrated superior performance compared to the base `AraBERT` model on both the validation and test datasets, confirming its suitability for social media text[cite: 81, 83].

---

## 🚀 How to Reproduce

Please follow the steps below to reproduce our results.

### Environment and Dependencies

[cite_start]The system was developed and tested on **Kaggle Notebooks (free tier)** with the following configuration[cite: 65]:
* [cite_start]**GPU**: 1x NVIDIA Tesla P100 16GB [cite: 65, 66]
* [cite_start]**RAM**: 13GB [cite: 66]
* [cite_start]**Python**: 3.11 [cite: 66]
* **Key Libraries**:
    * [cite_start]`PyTorch 2.6.0` [cite: 66]
    * [cite_start]`Transformers 4.52.4` [cite: 66]
    * [cite_start]`Optuna 4.4.0` [cite: 66]

You can install all required dependencies by running:
```bash
pip install -r requirements.txt
