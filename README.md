# Credit Card Fraud Detection

![R](https://img.shields.io/badge/R-276DC3?style=for-the-badge&logo=r&logoColor=white)
![RMarkdown](https://img.shields.io/badge/RMarkdown-276DC3?style=for-the-badge&logo=r&logoColor=white)
![Tidyverse](https://img.shields.io/badge/Tidyverse-1A162D?style=for-the-badge&logo=r&logoColor=white)

**Can machine learning reliably detect fraudulent credit card transactions?**  
End-to-end fraud detection pipeline in R — EDA, class balancing, logistic regression, random forest, and business-oriented threshold analysis on 1M transactions.

---

## ✅ Recommendation: Logistic Regression for Production, RF for Batch Scoring

> Logistic regression offers full interpretability — critical in regulated environments where you need to explain why a transaction was flagged. Random forest achieves higher raw accuracy (confirmed via cross-validation) and works well for automated batch scoring on high-value transactions.

| Model | Accuracy | Precision | Recall | F1 | Interpretable |
|-------|----------|-----------|--------|----|---------------|
| Logistic Regression | ~93% | — | — | — | Yes |
| Random Forest (3-fold CV) | ~99% | — | — | — | No |

---

## 🔍 Key Findings

- **PIN usage** is the strongest fraud signal — fraud rate drops from 9.7% to 0.27% when PIN is used
- **Online orders** are ~10x more likely to be fraudulent (12.7% vs 1.3%)
- **repeat_retailer** alone shows almost no effect — but its interaction with `distance_from_home` is statistically significant (LRT p < 0.05)
- RF near-perfect accuracy confirmed stable via 3-fold cross-validation — not overfitting
- Lowering the decision threshold from 0.5 → 0.3 significantly improves recall at the cost of precision — a business tradeoff depending on transaction value

---

## 🔬 Analysis Pipeline

```
Step  Task
----  ----
1     Load and explore 1M transaction dataset
2     EDA — distributions, fraud rates by variable, correlation matrix
3     Class balancing — bootstrapping minority class (8.74% fraud rate)
4     Train/test split — 70/30
5     Logistic regression — backward elimination for feature selection
6     Interaction term — tested via Likelihood Ratio Test
7     Model evaluation — accuracy, precision, recall, F1, AUC/ROC
8     Random Forest — ranger implementation, feature importance
9     Cross-validation — 3-fold CV to validate RF accuracy
10    Example predictions — Low Risk vs High Risk vs Borderline transactions
11    Threshold analysis — precision/recall tradeoff across 0.3–0.7
12    Model comparison + final recommendation + next steps
```

---

## 📐 Methods Reference

| Method | Purpose |
|--------|---------|
| Bootstrapping | Balance 8.74% minority fraud class before modeling |
| Backward elimination (AIC) | Identify most informative predictors |
| Logistic Regression | Interpretable baseline classifier |
| Likelihood Ratio Test | Compare base vs interaction model |
| ROC / AUC | Evaluate discrimination across all thresholds |
| Random Forest (ranger) | Ensemble method for non-linear patterns |
| Feature importance (impurity) | Understand which variables drive RF predictions |
| 3-fold Cross-validation | Validate RF accuracy, rule out overfitting |
| Threshold analysis | Tune precision/recall tradeoff for business context |

---

## 💡 What I Would Do Next

1. **SMOTE** instead of bootstrapping for more realistic minority class augmentation
2. **XGBoost** — often outperforms RF on tabular fraud data with less tuning
3. **Real-time scoring pipeline** — wrap model in a REST API (Plumber in R or FastAPI in Python)
4. **Drift monitoring** — track model performance over time as fraud patterns evolve
5. **Cost-sensitive learning** — assign different misclassification costs based on transaction value

---

## 📂 Folder Structure

```
credit-card-fraud-detection/
│
├── README.md
├── credit_card_fraud.Rmd
├── credit_card_fraud.html
├── install_packages.R
└── .gitignore
```

---

## ▶️ How to Run

```r
# 1. Install required packages
source("install_packages.R")

# 2. Download dataset from Kaggle and place in working directory
# https://www.kaggle.com/datasets/dhanushnarayananr/credit-card-fraud
# File needed: card_transdata.csv

# 3. Knit the R Markdown file in RStudio
# Click Knit → Knit to HTML
```

---

## 🗂️ Dataset

[Credit Card Fraud — Kaggle](https://www.kaggle.com/datasets/dhanushnarayananr/credit-card-fraud)

| File | Rows | Description |
|------|------|-------------|
| card_transdata.csv | 1,000,000 | Transaction records with 7 features + fraud label |

---

## ⚠️ Note on Data

- Dataset is synthetic — real-world fraud patterns are more complex and evolving
- `card_transdata.csv` is excluded from this repo (see `.gitignore`) — download directly from Kaggle

---

## 🏷️ Skills Demonstrated

`R` `R Markdown` `Logistic Regression` `Random Forest` `Feature Engineering`  
`Class Imbalance Handling` `Bootstrapping` `Cross-Validation` `ROC/AUC`  
`Threshold Analysis` `Business Impact Analysis` `EDA` `Data Visualization`  
`ggplot2` `ranger` `caret`

---

## 👤 Author

**Suin Kim** — M.S. Statistics & Data Science, Baruch College  
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://linkedin.com/in/suinkim29)
[![Email](https://img.shields.io/badge/Email-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:suin.kim29@gmail.com)