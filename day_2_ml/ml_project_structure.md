# IBM HR Attrition — Machine Learning Project Summary

## Project Completed

This project focused on building a complete machine learning workflow using the **IBM HR Analytics Employee Attrition dataset**.

## Work Completed

### 1. Project Setup

- Kaggle dataset setup
- Data loading
- Initial dataset inspection

### 2. Exploratory Data Analysis

- Professional EDA charts
- Attrition distribution analysis
- Department, job role, overtime, age, income, tenure, satisfaction, and work-life balance analysis
- Final EDA summary with high-risk employee segments

### 3. Data Preprocessing

- Train-test split
- Numeric and categorical feature separation
- Missing value handling
- Scaling techniques:
  - `StandardScaler`
  - `MinMaxScaler`
  - `RobustScaler`
- Categorical encoding using `OneHotEncoder`

### 4. Machine Learning Pipeline

- `Pipeline`
- `ColumnTransformer`
- Logistic Regression baseline model

### 5. Model Evaluation

- Confusion matrix
- Accuracy
- Precision
- Recall
- F1-score
- ROC-AUC
- PR-AUC
- Precision-Recall curve
- ROC curve

### 6. Feature Engineering

- Custom Transformer using `BaseEstimator` and `TransformerMixin`
- Engineered feature:
  - `JobSatisfaction_x_YearsAtCompany`

### 7. Encoding Experiment

- `TargetEncoder`
- Data leakage explanation
- Pipeline-based leakage control

### 8. Model Experiments

- Scaler comparison
- Random Forest model
- Random Forest threshold tuning
- XGBoost installation and model training

### 9. Final Model Comparison

Compared multiple model approaches:

- Logistic Regression with MinMaxScaler
- Random Forest default threshold
- Random Forest tuned threshold
- XGBoost

### 10. Final Selected Model

The final selected model was:

> **Random Forest with prediction threshold = 0.25**

This model was selected because it provided the best business balance for employee attrition prediction.

| Metric | Score |
|---|---:|
| Accuracy | 80.0% |
| Precision | 42.7% |
| Recall | 70.4% |
| F1-score | 53.2% |

## Final Business Conclusion

The final model can be used as an **HR early-warning system** to identify employees who may be at higher risk of leaving.

The model should support HR decision-making, not replace it. Predictions should be combined with business context, manager feedback, employee conversations, and ethical HR judgment.

## Supporting Material

- Final project notebook
- Foundation learning PDF/manual
- Professional charts and model comparison visuals