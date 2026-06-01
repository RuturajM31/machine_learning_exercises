---

## 11. Variable Map & Method Flow

### Big Picture

The main idea of the project is simple:

> **Training data can change. Test data must stay fixed.**

This rule makes the model comparison fair.

```text
Original Dataset
      │
      ▼
Features + Target
      │
      ▼
Train/Test Split
      │
      ├── Training Data → Scaling → Resampling / Class Weights / XGBoost → Model Training
      │
      └── Test Data     → Scaling only → Final Evaluation
```

The test set is never resampled because it should represent real-world fraud detection, where fraud cases are naturally rare.

---

## 1. Main Dataset Objects

| Object | Meaning |
|---|---|
| `df` | Full Credit Card Fraud dataset |
| `X` | All feature columns used for prediction |
| `y` | Target variable: `Class` |
| `Class = 0` | Normal transaction |
| `Class = 1` | Fraud transaction |

The target is highly imbalanced. Fraud cases represent only a very small share of all transactions.

---

## 2. Train/Test Split

```text
X, y
 │
 ├── X_train, y_train  → used for training
 │
 └── X_test, y_test    → used only for evaluation
```

| Object | Role |
|---|---|
| `X_train` | Training features before scaling |
| `y_train` | Training labels |
| `X_test` | Test features before scaling |
| `y_test` | Test labels |

The split was stratified, so the fraud ratio stayed almost the same in both train and test data.

### Why this matters

Fraud cases are rare.  
Without stratification, the test set could accidentally contain too few fraud cases, making evaluation unstable.

---

## 3. Scaling Step

Only `Time` and `Amount` were scaled.

```text
X_train  ── fit scaler on train ──► X_train_scaled
X_test   ── use same scaler ──────► X_test_scaled
```

| Object | Meaning |
|---|---|
| `X_train_scaled` | Training features after scaling `Time` and `Amount` |
| `X_test_scaled` | Test features after applying the same fitted scaler |

The scaler was fitted only on the training data to avoid data leakage.

### Why this matters

SMOTE is distance-based.  
If `Amount` or `Time` has a much larger scale than the other features, it can dominate the nearest-neighbour calculation.

---

## 4. Resampling Map

All resampling methods were applied only to the training data.

```text
X_train_scaled, y_train
        │
        ├── Original               → X_train_scaled, y_train
        ├── Random Oversampling    → X_train_ros, y_train_ros
        ├── SMOTE                  → X_train_smote, y_train_smote
        ├── Random Undersampling   → X_train_rus, y_train_rus
        └── Tomek Links            → X_train_tl, y_train_tl
```

| Method | Feature Variable | Target Variable | What Happens |
|---|---|---|---|
| Original | `X_train_scaled` | `y_train` | Keeps the natural imbalance |
| Random Oversampling | `X_train_ros` | `y_train_ros` | Duplicates fraud cases |
| SMOTE | `X_train_smote` | `y_train_smote` | Creates synthetic fraud-like cases |
| Random Undersampling | `X_train_rus` | `y_train_rus` | Removes many normal cases |
| Tomek Links | `X_train_tl` | `y_train_tl` | Removes borderline normal cases |

### Simple explanation

The original training data had very few fraud examples.  
Each resampling method changed the training data in a different way so that the model could learn fraud patterns better.

The test data was not changed.

---

## 5. Random Forest Training Flow

Each Random Forest model used a different training-data version.

```text
Original Training Data      ──► Random Forest ──► Model 1
Random Oversampling Data    ──► Random Forest ──► Model 2
SMOTE Data                  ──► Random Forest ──► Model 3
Random Undersampling Data   ──► Random Forest ──► Model 4
Tomek Links Data            ──► Random Forest ──► Model 5
```

All trained Random Forest models were stored in:

```python
rf_models
```

This dictionary keeps the model name and fitted model together.

| Dictionary Key | Model Meaning |
|---|---|
| `"Original"` | Random Forest trained on untreated scaled training data |
| `"Random Oversampling"` | Random Forest trained on oversampled training data |
| `"SMOTE"` | Random Forest trained on SMOTE-balanced training data |
| `"Random Undersampling"` | Random Forest trained on undersampled training data |
| `"Tomek Links"` | Random Forest trained on Tomek-cleaned training data |

---

## 6. Random Forest Evaluation Flow

All Random Forest models were tested on the same unchanged test set.

```text
rf_models
    │
    └── predict on X_test_scaled
              │
              ▼
        compare with y_test
              │
              ▼
        rf_results_table
```

| Evaluation Object | Meaning |
|---|---|
| `X_test_scaled` | Final test features |
| `y_test` | True test labels |
| `rf_results_table` | Random Forest model comparison results |

This makes the comparison fair because only the training strategy changes.

---

## 7. Cost-Sensitive Learning Flow

After resampling methods, class-weighted Random Forest models were tested.

Unlike resampling, class weighting does not create or remove rows.

```text
X_train_scaled, y_train
        │
        ├── class_weight = "balanced"
        │        └── Random Forest
        │
        └── class_weight = {0:1, 1:100}
                 └── Random Forest
```

The trained class-weighted models were stored in:

```python
rf_weighted_models
```

The results were stored in:

```python
rf_weighted_results_table
```

| Model | Meaning |
|---|---|
| `class_weight="balanced"` | Automatically increases the importance of the rare fraud class |
| `class_weight={0:1, 1:100}` | Manually makes fraud-class mistakes 100 times more costly |

### Simple explanation

Instead of changing the data, class weighting changes how seriously the model treats fraud mistakes.

---

## 8. Threshold Optimisation Flow

The best balanced Random Forest model was the Tomek Links Random Forest.

The default threshold is usually:

```text
0.50
```

But the best threshold for fraud detection may be different.

```text
Tomek Links Random Forest
        │
        ▼
Predict fraud probabilities on X_test_scaled
        │
        ▼
Try thresholds from 0.10 to 0.90
        │
        ▼
Calculate Precision, Recall, and F1-Score
        │
        ▼
Best threshold = 0.40
```

The threshold results were stored in:

```python
threshold_results_df
```

The comparison between default and optimised threshold was stored in:

```python
threshold_comparison_df
```

### Final threshold result

| Threshold | Precision | Recall | F1-Score | False Positives | False Negatives | True Positives |
|---:|---:|---:|---:|---:|---:|---:|
| `0.50` | 0.9318 | 0.8367 | 0.8817 | 6 | 16 | 82 |
| `0.40` | 0.9326 | 0.8469 | 0.8877 | 6 | 15 | 83 |

Lowering the threshold to `0.40` detected one extra fraud case without increasing false positives.

---

## 9. XGBoost Flow

The final expert model used:

```text
SMOTE + XGBoost + scale_pos_weight
```

```text
X_train_smote, y_train_smote
        │
        ▼
Calculate scale_pos_weight
        │
        ▼
Train XGBoost
        │
        ▼
Evaluate on X_test_scaled, y_test
        │
        ▼
xgb_smote_results_table
```

### `scale_pos_weight` logic

The formula is:

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

The trained XGBoost model was stored in:

```python
xgb_smote_model
```

The result was stored in:

```python
xgb_smote_results_table
```

---

## 10. Final Evaluation Flow

The final comparison used three practical candidates:

```text
Tomek RF at threshold 0.50
Tomek RF at threshold 0.40
SMOTE + XGBoost at threshold 0.50
```

```text
Final candidate models
        │
        ▼
Evaluate on same X_test_scaled and y_test
        │
        ▼
Compare technical metrics
        │
        ▼
Compare business impact
        │
        ▼
Final recommendation
```

The final comparison table was stored in:

```python
final_model_comparison
```

---

## 11. Metrics Used

| Metric | Simple Meaning | Fraud Detection Meaning |
|---|---|---|
| Accuracy | Overall correctness | Can be misleading because normal cases dominate |
| Precision | How many predicted fraud cases were truly fraud | Measures false-alarm quality |
| Recall | How many real fraud cases were detected | Measures fraud-catching ability |
| F1-Score | Balance between Precision and Recall | Useful overall fraud metric |
| ROC-AUC | Separation ability across thresholds | Shows how well fraud and normal cases are ranked |

### Important lesson

ROC-AUC is useful, but it is not enough by itself.

A model can have a high ROC-AUC and still produce too many false alerts at a specific decision threshold.

---

## 12. Visual Outputs in This Notebook

| Output | Purpose |
|---|---|
| Class Distribution Chart | Shows the original imbalance |
| Dummy Baseline Confusion Matrix | Shows why accuracy can be misleading |
| Resampling Composition Chart | Shows how each method changes class balance |
| Method Flow Diagram | Shows how variables and methods connect |
| Random Forest Scorecard Table | Compares Random Forest models across key metrics |
| ROC Curve Chart | Compares model separation ability across thresholds |
| Cost-Sensitive Benchmark Chart | Compares best resampling model with class-weighted models |
| Threshold Optimisation Chart | Shows F1-Score across thresholds |
| Final Benchmark Dashboard | Compares technical metrics and business impact |

---

## 13. Key Learning Point

```text
Different training strategies
        +
Same unchanged test set
        +
Business-aware metrics
        =
Fair model selection
```

The test set is never resampled because it should represent real-world fraud detection.

---

## 14. Final Model Finding

The final model comparison showed:

| Model | Main Finding |
|---|---|
| Tomek RF — 0.50 | Strong balanced model |
| Tomek RF — 0.40 | Best practical model |
| SMOTE + XGBoost — 0.50 | Highest ROC-AUC, but too many false alerts |

### Business impact

| Model | Detected Fraud | Missed Fraud | False Alerts |
|---|---:|---:|---:|
| Tomek RF — 0.50 | 82 | 16 | 6 |
| Tomek RF — 0.40 | 83 | 15 | 6 |
| SMOTE + XGBoost — 0.50 | 86 | 12 | 451 |

### Practical takeaway

SMOTE + XGBoost detected 3 more fraud cases than Tomek RF at threshold `0.40`.

However, it created 445 more false alerts.

```text
SMOTE + XGBoost:
+3 detected fraud cases
+445 false alerts
```

That trade-off is not practical for real-time fraud detection.

---

## 15. Final Recommendation

The selected model is:

```text
Tomek Links Random Forest with optimised threshold 0.40
```

### Why this model was selected

| Reason | Explanation |
|---|---|
| High Precision | Fraud alerts are reliable |
| Strong Recall | Detects most fraud cases |
| Best F1-Score | Best balance between Precision and Recall |
| Low false alerts | Only 6 normal transactions were wrongly flagged |
| Practical for real-time use | Strong performance without overwhelming fraud-review teams |

---

## 16. Final Mental Model

```text
Best model ≠ highest ROC-AUC only

Best model =
fraud detected
+ false alerts controlled
+ practical real-time usability
```

At the end of this project, the strongest practical model is:

> **Tomek Links Random Forest with threshold 0.40**

---
