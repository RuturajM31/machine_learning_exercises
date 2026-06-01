# Learning Day 3 — Imbalanced Data  
## Final Project Workflow Steps

**Project:** Credit Card Fraud Detection  
**Main topic:** Imbalanced classification  
**Current status:** Completed project workflow  
**Final practical model:** Tomek Links Random Forest with optimised threshold `0.40`

---

## 1. Big Picture

The goal of this project was to understand how machine learning models behave when the class we care about is extremely rare.

In this dataset:

| Class | Meaning |
|---:|---|
| `0` | Normal transaction |
| `1` | Fraud transaction |

Fraud cases are very rare. Because of this, a model can show very high accuracy while still missing fraud cases.

That is why this project focused mainly on **Precision**, **Recall**, **F1-Score**, **ROC-AUC**, confusion matrix results, and business impact. Accuracy was included, but it was not treated as the main decision metric.

---

## 2. Core Rule of the Project

> **Training data can change. Test data must stay unchanged.**

```text
Original data
   ↓
Train/test split
   ↓
Training data → scaling → resampling → model training
Test data     → scaling only → final evaluation
```

The test set was never resampled. This is important because the test set should represent real-world fraud detection, where fraud cases are naturally rare.

---

## 3. Full Project Steps Completed

| Step | What We Did | Why It Matters |
|---:|---|---|
| 1 | Cleared theory concepts | Understood imbalance, minority class, metrics, thresholds, and leakage |
| 2 | Loaded the dataset | Used KaggleHub logic with local CSV fallback |
| 3 | Inspected the dataset | Checked rows, columns, missing values, data types, and duplicates |
| 4 | Checked class distribution | Confirmed fraud is only about **0.17%** of the data |
| 5 | Built dummy baseline | Proved that high accuracy can still miss all fraud cases |
| 6 | Split train/test data | Used stratification to preserve the fraud ratio |
| 7 | Scaled `Time` and `Amount` | Prepared data for distance-based methods such as SMOTE |
| 8 | Applied Random Oversampling | Duplicated fraud cases to balance training data |
| 9 | Applied SMOTE | Created synthetic fraud-like examples |
| 10 | Applied Random Undersampling | Reduced normal transactions to balance training data |
| 11 | Applied Tomek Links | Removed borderline normal transactions near fraud cases |
| 12 | Compared resampled datasets | Checked how each method changed class balance |
| 13 | Created evaluation function | Built reusable function for Accuracy, Precision, Recall, F1, and ROC-AUC |
| 14 | Trained Random Forest models | Trained one model per training-data version |
| 15 | Evaluated Random Forest models | Tested all models on the same unchanged test set |
| 16 | Plotted ROC curves | Compared model separation ability across thresholds |
| 17 | Trained class-weighted Random Forest models | Tested cost-sensitive learning |
| 18 | Compared class-weighted models | Compared `class_weight="balanced"` and `{0:1, 1:100}` |
| 19 | Performed threshold optimisation | Tested thresholds from `0.10` to `0.90` |
| 20 | Selected best threshold | Found best F1-Score at threshold `0.40` |
| 21 | Trained SMOTE + XGBoost | Tested advanced boosting approach |
| 22 | Evaluated SMOTE + XGBoost | Compared against best Random Forest model |
| 23 | Created final benchmark dashboard | Compared technical metrics and business impact |
| 24 | Made final recommendation | Selected the best practical model for real-time fraud detection |

---

## 4. Simple Variable Map

### Main Data Objects

| Variable | Meaning |
|---|---|
| `df` | Full dataset |
| `X` | All feature columns |
| `y` | Target column: `Class` |

### Train/Test Split

| Variable | Meaning |
|---|---|
| `X_train` | Training features before scaling |
| `X_test` | Test features before scaling |
| `y_train` | Training labels |
| `y_test` | Test labels |

### Scaled Data

| Variable | Meaning |
|---|---|
| `X_train_scaled` | Training features after scaling `Time` and `Amount` |
| `X_test_scaled` | Test features after applying the same scaler |

### Resampled Training Data

| Method | Feature Variable | Target Variable |
|---|---|---|
| Original | `X_train_scaled` | `y_train` |
| Random Oversampling | `X_train_ros` | `y_train_ros` |
| SMOTE | `X_train_smote` | `y_train_smote` |
| Random Undersampling | `X_train_rus` | `y_train_rus` |
| Tomek Links | `X_train_tl` | `y_train_tl` |

### Model and Results Objects

| Variable | Meaning |
|---|---|
| `rf_models` | Dictionary containing Random Forest models trained on resampled data versions |
| `rf_results_table` | Random Forest metric comparison table |
| `rf_weighted_models` | Dictionary containing class-weighted Random Forest models |
| `rf_weighted_results_table` | Class-weighted Random Forest results |
| `threshold_results_df` | Threshold optimisation results |
| `threshold_comparison_df` | Default vs optimised threshold comparison |
| `xgb_smote_model` | SMOTE + XGBoost model |
| `xgb_smote_results_table` | SMOTE + XGBoost result table |
| `final_model_comparison` | Final comparison table of the best practical models |

---

## 5. Method Flow

The same Random Forest model type was trained on different versions of the training data.

```text
X_train_scaled + y_train
        │
        ├── Original Random Forest
        ├── Random Oversampling Random Forest
        ├── SMOTE Random Forest
        ├── Random Undersampling Random Forest
        └── Tomek Links Random Forest
```

All models were evaluated using the same test data:

```text
X_test_scaled + y_test
```

This made the comparison fair.

---

## 6. Resampling Methods Used

| Method | Simple Meaning | Main Risk |
|---|---|---|
| Random Oversampling | Copies fraud cases until classes are balanced | May cause overfitting |
| SMOTE | Creates synthetic fraud-like cases | May create unrealistic examples |
| Random Undersampling | Removes many normal cases | May lose important normal patterns |
| Tomek Links | Removes confusing majority samples near fraud | Does not fully balance the dataset |

### Resampling Result Summary

| Method | Normal Count | Fraud Count | Fraud Percentage |
|---|---:|---:|---:|
| Original Training Data | 227,451 | 394 | 0.1729% |
| Random Oversampling | 227,451 | 227,451 | 50.0000% |
| SMOTE | 227,451 | 227,451 | 50.0000% |
| Random Undersampling | 394 | 394 | 50.0000% |
| Tomek Links | 227,431 | 394 | 0.1729% |

---

## 7. Random Forest Model Comparison

The Random Forest models were compared using Accuracy, Precision, Recall, F1-Score, and ROC-AUC.

| Model | Accuracy | Precision | Recall | F1-Score | ROC-AUC |
|---|---:|---:|---:|---:|---:|
| Random Forest — Original | 0.9996 | 0.9412 | 0.8163 | 0.8743 | 0.9533 |
| Random Forest — Random Oversampling | 0.9996 | 0.9625 | 0.7857 | 0.8652 | 0.9583 |
| Random Forest — SMOTE | 0.9995 | 0.8602 | 0.8163 | 0.8377 | 0.9703 |
| Random Forest — Random Undersampling | 0.9634 | 0.0411 | 0.9082 | 0.0787 | 0.9774 |
| Random Forest — Tomek Links | 0.9996 | 0.9419 | 0.8265 | 0.8804 | 0.9583 |

### Random Forest Observations

| Result | Interpretation |
|---|---|
| Tomek Links had the best F1-Score | Best balance between detecting fraud and controlling false alarms |
| Random Undersampling had the highest Recall | Detected many fraud cases |
| Random Undersampling had very low Precision | Created too many false alarms |
| Original Random Forest was already strong | Random Forest handled imbalance reasonably well |
| SMOTE improved ROC-AUC | Good separation ability, but lower Precision |

---

## 8. ROC Curve Results

ROC curves compared how well the Random Forest models separate fraud from normal transactions across thresholds.

| Model | ROC-AUC |
|---|---:|
| Random Forest — Original | 0.9533 |
| Random Forest — Random Oversampling | 0.9583 |
| Random Forest — SMOTE | 0.9703 |
| Random Forest — Random Undersampling | 0.9774 |
| Random Forest — Tomek Links | 0.9583 |

Random Undersampling had the highest ROC-AUC among the Random Forest variants, but its Precision was extremely low. This showed that ROC-AUC alone is not enough for the final business decision.

---

## 9. Cost-Sensitive Learning

Cost-sensitive learning was tested using class weights. Unlike resampling, class weighting does not create or remove rows. It keeps the original training data but changes the penalty for mistakes on the fraud class.

| Model | Accuracy | Precision | Recall | F1-Score | ROC-AUC |
|---|---:|---:|---:|---:|---:|
| Random Forest — Balanced Class Weight | 0.9995 | 0.9600 | 0.7347 | 0.8324 | 0.9534 |
| Random Forest — Manual Class Weight 1:100 | 0.9995 | 0.9737 | 0.7551 | 0.8506 | 0.9584 |

The manual class-weight setting performed better than the automatic balanced setting, but it did not outperform the best resampling-based Random Forest.

---

## 10. Threshold Optimisation

The best Random Forest model before threshold tuning was:

```text
Tomek Links Random Forest
```

Thresholds from `0.10` to `0.90` were tested. The goal was to find the threshold that maximised F1-Score.

| Threshold | F1-Score |
|---:|---:|
| Default threshold `0.50` | 0.8817 |
| Optimised threshold `0.40` | 0.8877 |

### Default vs Optimised Threshold

| Threshold | Precision | Recall | F1-Score | False Positives | False Negatives | True Positives |
|---:|---:|---:|---:|---:|---:|---:|
| `0.50` | 0.9318 | 0.8367 | 0.8817 | 6 | 16 | 82 |
| `0.40` | 0.9326 | 0.8469 | 0.8877 | 6 | 15 | 83 |

Lowering the threshold from `0.50` to `0.40` detected one extra fraud case without increasing false positives.

---

## 11. SMOTE + XGBoost + `scale_pos_weight`

XGBoost was tested as the final expert model.

| Component | Purpose |
|---|---|
| SMOTE | Creates synthetic fraud-like examples |
| XGBoost | Trains a strong boosting model |
| `scale_pos_weight` | Controls class importance |

### `scale_pos_weight` Calculation

```text
scale_pos_weight = number of normal transactions / number of fraud transactions
```

Before SMOTE:

```text
scale_pos_weight = 227,451 / 394 = 577.29
```

After SMOTE:

```text
scale_pos_weight = 227,451 / 227,451 = 1.00
```

Because SMOTE already balanced the training data, the XGBoost model used:

```python
scale_pos_weight = 1.0
```

### SMOTE + XGBoost Result

| Model | Accuracy | Precision | Recall | F1-Score | ROC-AUC |
|---|---:|---:|---:|---:|---:|
| SMOTE + XGBoost | 0.9919 | 0.1601 | 0.8776 | 0.2709 | 0.9813 |

SMOTE + XGBoost achieved the highest ROC-AUC and caught many fraud cases. However, its Precision was very low, meaning it created too many false alerts.

---

## 12. Final Model Comparison

| Model | Accuracy | Precision | Recall | F1-Score | ROC-AUC |
|---|---:|---:|---:|---:|---:|
| Tomek Links RF — Default Threshold 0.50 | 0.9996 | 0.9318 | 0.8367 | 0.8817 | 0.9583 |
| Tomek Links RF — Optimised Threshold 0.40 | 0.9996 | 0.9326 | 0.8469 | 0.8877 | 0.9583 |
| SMOTE + XGBoost — Default Threshold 0.50 | 0.9919 | 0.1601 | 0.8776 | 0.2709 | 0.9813 |

### Business Impact on Test Set

| Model | Detected Fraud | Missed Fraud | False Alerts |
|---|---:|---:|---:|
| Tomek Links RF — 0.50 | 82 | 16 | 6 |
| Tomek Links RF — 0.40 | 83 | 15 | 6 |
| SMOTE + XGBoost — 0.50 | 86 | 12 | 451 |

---

## 13. Final Recommendation

### Selected Model

```text
Tomek Links Random Forest with optimised threshold 0.40
```

### Why This Model Was Selected

| Reason | Explanation |
|---|---|
| High Precision | Fraud alerts are reliable |
| Strong Recall | Detects most fraud cases |
| Best F1-Score | Best balance between Precision and Recall |
| Low false alerts | Only 6 normal transactions were wrongly flagged |
| Practical for real-time use | Strong performance without overwhelming alert volume |

### Why SMOTE + XGBoost Was Not Selected

SMOTE + XGBoost had the highest ROC-AUC and detected more fraud cases.

However, it created **451 false alerts**.

Compared with Tomek Links RF at threshold `0.40`:

```text
SMOTE + XGBoost detects 3 more fraud cases
but creates 445 more false alerts
```

For real-time fraud detection, that trade-off is not practical.

---

## 14. Charts and Tables Created

| Output | Purpose |
|---|---|
| Class distribution chart | Shows how rare fraud cases are |
| Dummy baseline confusion matrix | Shows why accuracy is misleading |
| Resampling composition chart | Shows how each resampling method changes class balance |
| Method flow diagram | Explains how variables and methods connect |
| Random Forest scorecard table | Compares models using key metrics |
| ROC curve comparison | Compares separation ability across thresholds |
| Cost-sensitive benchmark chart | Compares best resampling model with class-weighted models |
| Threshold optimisation chart | Shows F1-Score across thresholds |
| Final benchmark dashboard | Compares technical metrics and business impact |

---

## 15. Final Mental Model

```text
Different training strategies
        +
Same unchanged test set
        +
Business-aware metrics
        =
Fair model selection
```

The purpose was not simply to get the highest score.

The purpose was to find a model that can:

- detect fraud cases,
- avoid too many false alarms,
- perform reliably on unseen data,
- and make sense for real-time fraud detection.

---

## 16. Final Learning Takeaway

The most important lesson from this project is:

> The best statistical model is not always the best business model.

SMOTE + XGBoost had the highest ROC-AUC, but its false-alert volume was too high.

The threshold-optimised Tomek Links Random Forest gave the best practical balance.

This makes it the most suitable model from this experiment for real-time fraud detection.

---

## 17. Explanation

If asked in an interview, this project can be explained like this:

> I worked on an imbalanced credit card fraud detection problem where fraud represented only about 0.17% of all transactions. I first showed why accuracy is misleading by building a dummy baseline that missed all fraud cases. Then I compared several imbalance-handling methods, including Random Oversampling, SMOTE, Random Undersampling, Tomek Links, class-weighted Random Forest, threshold optimisation, and SMOTE with XGBoost. I made sure resampling was applied only to the training data to avoid leakage. Although SMOTE + XGBoost achieved the highest ROC-AUC, it produced too many false alerts. The best practical model was Tomek Links Random Forest with an optimised threshold of 0.40, because it achieved the best F1-Score while keeping false positives very low.

---
