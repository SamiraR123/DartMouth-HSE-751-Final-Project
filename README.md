# Final Project: Socioeconomic Factors in Diabetes Risk Prediction
 
## Overview
This repository contains the final, end-to-end analytical pipeline for my HSE 751 final project: predicting diabetes/prediabetes risk from demographic, socioeconomic, behavioral, and health-status indicators, with particular interest in how much socioeconomic variables (income, education, healthcare access) contribute to that prediction alongside clinical and behavioral ones.

## Dataset
**Name:** CDC Diabetes Health Indicators

**Source:** UCI Machine Learning Repository, [https://archive.ics.uci.edu/dataset/891](https://archive.ics.uci.edu/dataset/891/cdc+diabetes+health+indicators)

**Size:** 253,680 respondents, 21 predictor variables, 1 binary target (`Diabetes_binary`)

The dataset is drawn from the CDC's 2015 Behavioral Risk Factor Surveillance System (BRFSS) survey and includes demographic, socioeconomic, behavioral, and self-reported health-status variables.

**Using a different dataset:** This notebook is built to run on any binary-classification dataset meeting the project's requirements (a binary target column, at least 300 rows, at least 10 predictor columns). The first cell in Part 1 prompts for a CSV upload, set `TARGET_COL` to your target column's name if using your own data. If nothing is uploaded, the notebook falls back to fetching the CDC dataset above directly from UCI.

## How to Run
1. Open `Final_Project_SR.ipynb` in Google Colab.
2. Run all cells in order, top to bottom.
3. When prompted in Part 1, either upload `cdc_diabetes_health_indicators.csv` (included in this repo) or click Cancel to let the notebook fetch the same dataset directly from UCI.
4. All profiling, validation, descriptive statistics, visualizations, inferential tests, model training, and evaluation regenerate automatically from that one data load.
No manual configuration is required beyond that initial upload prompt; all package installs (`ucimlrepo`) are handled inline within the notebook.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/17IPPd-SQ093PtxnKVFGPWwitsc1ml9UQ?usp=sharing)

## Notebook Contents
 
| Part | Contents |
|---|---|
| 1 | Formalizing the ML problem, dataset selection, upload/import, automated profiling, basic validation |
| 2 | Target and predictor descriptions, descriptive statistics, exploratory visualizations, correlation analysis |
| 3 | Automated data validation, BMI feature engineering, automated class-imbalance detection |
| 4 | Inferential statistics: chi-square test (Income) and Welch's t-test (BMI), both with effect sizes |
| 5 | Logistic Regression and Decision Tree: train/test split, preprocessing pipeline, both model formulas, training, evaluation function |
| 6 | Confusion matrices, metric comparison, ROC curves, decision threshold analysis, hyperparameter tuning, best model selection |
| 7 | Interpretation of findings and limitations |


## Key Findings
- Both Income (Cramer's V = 0.166) and BMI (Cohen's d = 0.641) show statistically significant, moderate-to-large associations with diabetes status.
- The target is imbalanced (~86% no diabetes, ~14% diabetes/prediabetes), which drives the choice of recall over accuracy as the primary evaluation metric.
- Decision Tree narrowly leads on recall (0.765); Logistic Regression leads on ROC AUC (0.820 vs. 0.808). The two metrics disagree, both are reported and reconciled in Part 6.6.
- Lowering the classification threshold from 0.5 to 0.3 raises recall from 76.1% to 91.7%, at a substantial cost to precision, a tradeoff discussed in Part 6.4 and Part 7.
  
## Limitations
See Part 7 of the notebook for a full discussion, including self-report bias, the single 2015 survey year, the absence of a race/ethnicity variable, and the lack of survey weighting in this cleaned dataset version.
 
## Dependencies
- pandas, numpy, matplotlib, seaborn
- scipy (chi2_contingency, ttest_ind, levene)
- scikit-learn (model_selection, linear_model, tree, metrics, preprocessing, compose, pipeline)
- statsmodels
- ucimlrepo (installed inline in the notebook if the default dataset is used)


## GenAI Disclosure
AI assistance (Claude) was used to help with the python code, strengthen the writeups, and organize this README. All data decisions, code execution, and final analysis are my own.
