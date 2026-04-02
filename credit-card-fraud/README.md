# Credit Card Fraud Detection with XGBoost and Optuna

## Overview
This project builds a machine learning model to detect fraudulent credit card transactions using **XGBoost**, optimized with **Optuna** hyperparameter tuning. The evaluation metric is **PR AUC (Precision-Recall Area Under Curve)**, which is more appropriate than ROC AUC for highly imbalanced datasets.

## Dataset
- **Source:** [Kaggle — Credit Card Fraud Detection](https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud)
- **Size:** 284,807 transactions, of which only 0.17% are fraudulent
- **Features:** 28 PCA-transformed components (V1–V28), plus `Time` and `Amount`
- **Target:** `Class` (0 = legitimate, 1 = fraud)

> The dataset is not included in this repository due to its size. Please download it from Kaggle and place `creditcard.csv` in the project directory.

## Why PR AUC over ROC AUC?
The dataset is severely imbalanced (0.17% fraud). A naive model predicting all transactions as legitimate would still achieve a ROC AUC close to 1.0, making it a misleading metric. PR AUC focuses on the minority class (fraud), providing a more honest evaluation of model performance.

## Results

| Model | PR AUC |
|-------|--------|
| Baseline XGBoost (30 trees) | 0.7900 |
| Tuned XGBoost (Optuna, 30 trials) | **0.8106** |

Optuna improved PR AUC by **+2.6%** over the baseline.

## Best Hyperparameters (Optuna)

| Parameter | Value |
|-----------|-------|
| `max_depth` | 5 |
| `learning_rate` | 0.0209 |
| `n_estimators` | 117 |
| `min_child_weight` | 3 |
| `gamma` | 0.0108 |
| `subsample` | 0.765 |
| `colsample_bytree` | 0.932 |
| `reg_alpha` | 0.0098 |
| `reg_lambda` | ~0 |

## Project Structure
```
├── ccfraud.ipynb       # Main notebook
├── ccfraud.py          # Python script version
├── README.md
└── .gitignore
```

## Requirements
```
xgboost
scikit-learn
optuna
pandas
numpy
matplotlib
```

Install dependencies:
```bash
pip install xgboost scikit-learn optuna pandas numpy matplotlib
```

## Usage
1. Download `creditcard.csv` from Kaggle and place it in this directory
2. Open `ccfraud.ipynb` in Jupyter or VS Code
3. Run all cells
