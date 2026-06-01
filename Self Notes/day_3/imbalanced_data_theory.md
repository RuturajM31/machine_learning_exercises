# Learning Day 3 — Imbalanced Data

**Module:** Machine Learning  
**Topic:** Imbalanced Data  
**Dataset:** Credit Card Fraud Detection  
**Target column:** `Class`  
**Main business problem:** Detect rare fraud transactions without being misled by high overall accuracy.

---

## 1. Why This Topic Matters

In many real-world machine learning problems, the class we care about most is rare. Examples include:

- Credit card fraud detection
- Medical diagnosis
- Customer churn prediction
- Loan default prediction
- Machine failure detection
- Security and anomaly detection

In these problems, the rare class is often the most important class.

For the Credit Card Fraud dataset:

| Class | Meaning | Role |
|---:|---|---|
| `0` | Normal transaction | Majority class |
| `1` | Fraud transaction | Minority class / positive class |

The full dataset contains:

| Class | Count | Percentage |
|---:|---:|---:|
| `0` | 284,315 | 99.827% |
| `1` | 492 | 0.173% |

This means fraud cases are extremely rare. If a model simply predicts every transaction as normal, it can still achieve very high accuracy, but it will catch no fraud.

That is the core danger of imbalanced data.

---

## Instructor Document Highlights — Simple Version

The uploaded theory material adds several important points that guide this Day 3 exercise.

### What the instructor material focuses on

The theory session is structured around:

- Introduction to imbalanced data
- Evaluation metrics
- Methods for imbalanced learning
- Sampling algorithms
- Kaggle-style dataset evaluation
- Final summary and practical takeaways

Simple meaning:

> First understand the imbalance problem, then choose better metrics, then compare different correction strategies.

### Formal idea in simple words

Imbalanced learning is about building useful decision boundaries when the target classes are strongly skewed.

In simple words:

> The model must learn the rare class even though it has very few examples.

This is difficult because standard ML algorithms usually try to minimise total errors. If the majority class dominates the dataset, the model can reduce total error by focusing mostly on the majority class.

### Common real-world examples

The instructor material highlights examples such as:

- Fraud detection
- Anomaly detection
- Cancer diagnosis
- Credit default prediction

In all of these cases, the rare event is usually the event we care about most.

### Key warning from the slides

If a dataset has a 95:5 class ratio, a naive model can predict only the majority class and still reach 95% accuracy.

Simple meaning:

> High accuracy does not automatically mean the model is useful.

For fraud detection, a model can look excellent on accuracy while catching no fraud.

### Main method families

The instructor material groups imbalance solutions into three families:

| Method family | Simple idea | Example |
|---|---|---|
| Data preprocessing | Change the training data balance | Oversampling, undersampling, SMOTE, Tomek Links |
| Algorithm-specific methods | Change how the model treats mistakes | `class_weight`, `scale_pos_weight` |
| Ensemble methods | Combine multiple models | Random Forest, boosting models |

### Sampling methods from the instructor material

The theory material explains that simple random sampling has risks:

- Random oversampling can cause overfitting because the minority examples are duplicated.
- Random undersampling can remove useful majority-class information.
- k-nearest-neighbour-based methods try to be more selective.

This is why methods like SMOTE, Tomek Links, and NearMiss are important to understand.

### Cost-sensitive learning from the instructor material

The slides explain that in a 95:5 dataset, minority-class mistakes may contribute only a small part of the total loss.

Simple meaning:

> If fraud is rare, the model may not feel enough penalty when it misses fraud.

Class weighting fixes this by making minority-class errors more expensive. For example, if the class ratio is 95:5, the minority class can receive a much higher weight so that the model pays more attention to it.

### Kaggle evaluation lesson from the instructor material

The instructor material includes a Kaggle-style credit-risk example and shows that the right metric and the right imbalance strategy matter. In that example, using class weighting and SMOTE improved AUC.

Simple lesson for our project:

> Do not trust one metric or one model. Compare methods carefully and judge them using the right business objective.

### Practical note about tools

The theory slides mention that scikit-learn supports class weighting for some models, while sampling methods are usually handled through specialised imbalance-learning tools.

For our notebook, this means:

- `sklearn` will be used for modelling and metrics.
- `imblearn` will be used for resampling methods such as Random Oversampling, Random Undersampling, SMOTE, and Tomek Links.

---

## 2. Key Terminology

### Dataset

A dataset is the table of data used for analysis and modelling.

In this exercise, each row represents one credit card transaction.

### Feature

A feature is an input variable used by the model to make predictions.

In the Credit Card Fraud dataset, the features include:

- `Time`
- `Amount`
- `V1` to `V28`

The columns `V1` to `V28` are anonymised numerical features created using PCA-like transformation.

### Target Variable

The target variable is the column we want to predict.

Here, the target is:

```text
Class
```

### Binary Classification

Binary classification means the model predicts one of two possible classes.

Here:

```text
0 = Normal transaction
1 = Fraud transaction
```

### Majority Class

The majority class is the class with many observations.

In this dataset:

```text
Class 0 = Normal transaction = Majority class
```

### Minority Class

The minority class is the class with very few observations.

In this dataset:

```text
Class 1 = Fraud transaction = Minority class
```

### Positive Class

The positive class usually means the event we care most about detecting.

In this exercise:

```text
Positive class = Fraud = Class 1
```

### Negative Class

The negative class is the non-event or normal class.

In this exercise:

```text
Negative class = Normal transaction = Class 0
```

---

## 3. What Is Imbalanced Data?

A dataset is imbalanced when one class appears much more often than another class.

Example:

```text
Normal transactions: 99.8%
Fraud transactions:  0.2%
```

The model sees many examples of normal transactions but very few examples of fraud. Because of this, standard models may learn to focus mostly on the majority class and ignore the minority class.

In business terms:

> The model may become very good at recognising normal transactions but very poor at catching fraud.

---

## 4. Why Accuracy Can Be Misleading

Accuracy measures the percentage of correct predictions.

```text
Accuracy = Correct predictions / Total predictions
```

More formally:

```text
Accuracy = (TP + TN) / Total
```

Imagine we have 100,000 transactions:

| Transaction type | Count |
|---|---:|
| Normal | 99,800 |
| Fraud | 200 |

A naive model predicts:

```text
Every transaction is normal.
```

Then it gets:

```text
99,800 correct predictions out of 100,000
```

So accuracy is:

```text
99.8%
```

This looks excellent. But the model caught:

```text
0 fraud cases
```

So the model is useless for fraud detection.

### Business Interpretation

Accuracy answers:

> How many total predictions were correct?

But in fraud detection, the better question is:

> How many fraud cases did we catch?

That is why accuracy alone is dangerous in imbalanced datasets.

---

## 5. Confusion Matrix

A confusion matrix compares the actual class with the predicted class.

|  | Predicted Fraud | Predicted Normal |
|---|---:|---:|
| **Actual Fraud** | True Positive | False Negative |
| **Actual Normal** | False Positive | True Negative |

### True Positive — TP

The model predicts fraud, and the transaction is actually fraud.

```text
Actual = Fraud
Predicted = Fraud
```

Business meaning:

> Fraud was correctly detected.

### True Negative — TN

The model predicts normal, and the transaction is actually normal.

```text
Actual = Normal
Predicted = Normal
```

Business meaning:

> A normal customer transaction was correctly allowed.

### False Positive — FP

The model predicts fraud, but the transaction is actually normal.

```text
Actual = Normal
Predicted = Fraud
```

Business meaning:

> A good customer may be wrongly blocked or investigated.

### False Negative — FN

The model predicts normal, but the transaction is actually fraud.

```text
Actual = Fraud
Predicted = Normal
```

Business meaning:

> Fraud was missed.

In fraud detection, false negatives are usually very costly because real fraud passes through the system.

---

## 6. Precision

Precision answers:

> Of all transactions predicted as fraud, how many were actually fraud?

Formula:

```text
Precision = TP / (TP + FP)
```

Example:

A model flags 100 transactions as fraud. Out of those 100, only 20 are truly fraud.

```text
Precision = 20 / 100 = 20%
```

### Business Meaning

High precision means:

> When the model says fraud, it is usually correct.

Low precision means:

> The model creates many false fraud alerts.

In fraud detection, low precision can annoy customers and increase manual review workload.

---

## 7. Recall

Recall answers:

> Of all real fraud cases, how many did the model catch?

Formula:

```text
Recall = TP / (TP + FN)
```

Example:

There are 100 real fraud transactions. The model catches 80.

```text
Recall = 80 / 100 = 80%
```

### Business Meaning

High recall means:

> The model catches most fraud cases.

Low recall means:

> The model misses many fraud cases.

Recall is also called:

- Sensitivity
- True Positive Rate
- TPR

For fraud detection, recall is often very important because missing fraud is expensive.

---

## 8. F1-Score

F1-score combines precision and recall into one metric.

Formula:

```text
F1 = 2 × (Precision × Recall) / (Precision + Recall)
```

Simple meaning:

> F1 is high only when both precision and recall are reasonably good.

Why it matters:

- Accuracy can be misleading.
- Precision alone ignores missed fraud.
- Recall alone ignores false alarms.
- F1 balances precision and recall.

In this exercise, F1-score is important because we compare models under different imbalance-handling strategies.

---

## 9. Specificity, FPR, and FNR

These terms are useful for understanding ROC curves and business trade-offs.

### Specificity

Specificity answers:

> Of all real normal transactions, how many did the model correctly classify as normal?

Formula:

```text
Specificity = TN / (TN + FP)
```

### False Positive Rate — FPR

FPR answers:

> Of all real normal transactions, how many were wrongly flagged as fraud?

Formula:

```text
FPR = FP / (FP + TN)
```

Business meaning:

> High FPR means too many normal customers are disturbed.

### False Negative Rate — FNR

FNR answers:

> Of all real fraud transactions, how many were missed?

Formula:

```text
FNR = FN / (FN + TP)
```

Business meaning:

> High FNR means too much fraud escapes detection.

---

## 10. Probability Predictions and Decision Threshold

Many classifiers first output probabilities, not final class labels.

Example:

```text
Transaction A → fraud probability = 0.82
Transaction B → fraud probability = 0.31
Transaction C → fraud probability = 0.04
```

A common default threshold is 0.50:

```text
If probability >= 0.50 → predict fraud
If probability <  0.50 → predict normal
```

But in fraud detection, 0.50 may be too strict.

For example:

```text
Fraud probability = 0.31
```

At threshold 0.50:

```text
Prediction = Normal
```

At threshold 0.20:

```text
Prediction = Fraud
```

### Threshold Optimisation

Threshold optimisation means testing different cutoff values and choosing the one that gives the best result.

In this exercise, we test thresholds from:

```text
0.10 to 0.90
```

The best threshold depends on the business objective.

For fraud detection:

- Lower threshold → catches more fraud, but creates more false alarms.
- Higher threshold → fewer false alarms, but may miss more fraud.

---

## 11. ROC Curve

ROC means:

```text
Receiver Operating Characteristic
```

A ROC curve shows how the model performs across many thresholds.

It plots:

```text
True Positive Rate vs False Positive Rate
```

That means:

```text
Recall vs False Positive Rate
```

### Business Interpretation

The ROC curve shows:

> How much fraud we can catch while accepting different levels of false alarms.

---

## 12. AUC / ROC-AUC

AUC means:

```text
Area Under the Curve
```

ROC-AUC summarises the ROC curve into one number.

Simple meaning:

> ROC-AUC tells us how well the model separates fraud from normal transactions overall.

Interpretation:

| ROC-AUC | Meaning |
|---:|---|
| 0.50 | Random guessing |
| 0.70 | Some separation |
| 0.80 | Good separation |
| 0.90+ | Very strong separation |

Important point:

ROC-AUC is threshold-independent. It evaluates ranking quality across many thresholds.

### Important Warning

In extremely imbalanced problems, ROC-AUC can sometimes look good even when precision is weak. That is why we also check:

- Precision
- Recall
- F1-score
- Confusion matrix

---

## 13. Precision-Recall Curve and PR-AUC

This is an expert-level addition.

A Precision-Recall curve plots:

```text
Precision vs Recall
```

It focuses directly on the minority class.

For rare event detection, such as fraud detection, PR-AUC can sometimes be more informative than ROC-AUC because ROC-AUC includes a very large number of true negatives.

In this course exercise, ROC-AUC is required. But in real business or interviews, it is useful to mention PR-AUC as an additional metric for imbalanced classification.

---

## 14. Resampling

Resampling means changing the class distribution in the training data.

There are two main types:

| Type | Meaning |
|---|---|
| Oversampling | Add more minority-class examples |
| Undersampling | Remove majority-class examples |

The purpose is to help the model learn the minority class better.

Important rule:

> Resampling must be applied only to the training data, never before the train/test split.

---

## 15. Random Oversampling

Random oversampling duplicates examples from the minority class.

Example before oversampling:

```text
Normal: 10,000
Fraud:      50
```

Example after oversampling:

```text
Normal: 10,000
Fraud:  10,000
```

### Advantage

The model sees more fraud examples during training.

### Disadvantage

The model may memorise duplicated fraud cases.

This can lead to overfitting.

---

## 16. Random Undersampling

Random undersampling removes examples from the majority class.

Example before undersampling:

```text
Normal: 10,000
Fraud:      50
```

Example after undersampling:

```text
Normal: 50
Fraud:  50
```

### Advantage

The training data becomes balanced and smaller.

### Disadvantage

Useful majority-class information may be lost.

In fraud detection, this can be risky because normal transaction behaviour is diverse.

---

## 17. SMOTE

SMOTE means:

```text
Synthetic Minority Oversampling Technique
```

SMOTE creates new synthetic minority examples instead of simply duplicating existing ones.

Simple process:

1. Select a minority-class example.
2. Find its nearest minority-class neighbours.
3. Create a synthetic point between the selected example and one of its neighbours.

### Advantage

SMOTE can help the model learn a broader minority-class region.

### Disadvantages

SMOTE can create unrealistic synthetic examples if the minority class is noisy.

SMOTE is also distance-based, so feature scaling can matter.

### Business View

In fraud detection, SMOTE can help the model learn more fraud-like patterns. But we must still evaluate on the original untouched test set.

---

## 18. Tomek Links

Tomek Links are pairs of examples from different classes that are very close to each other.

Example:

```text
One normal transaction and one fraud transaction are nearest neighbours.
```

These examples are close to the decision boundary.

Tomek Links usually remove the majority-class example from such pairs.

### Simple Meaning

> Tomek Links clean the boundary between classes.

### Advantage

They remove confusing majority-class points near the minority class.

### Disadvantage

They usually do not fully balance the dataset.

Tomek Links are more of a cleaning method than a full balancing method.

---

## 19. NearMiss

NearMiss is an undersampling method.

Instead of randomly removing majority-class examples, it selects majority-class examples based on distance to minority-class examples.

Simple meaning:

> NearMiss keeps majority examples that are close to minority examples.

Why this can help:

These close examples are harder cases and help define the decision boundary.

There are three common versions:

| Method | Simple idea |
|---|---|
| NearMiss-1 | Keeps majority samples closest to nearby minority samples |
| NearMiss-2 | Uses distance to farthest minority samples |
| NearMiss-3 | Selects majority samples closest to each minority sample |

NearMiss appears in the instructor material, but the main Day 3 exercise focuses on Random Oversampling, SMOTE, Random Undersampling, and Tomek Links.

---

## 20. One-Sided Selection

One-Sided Selection combines multiple undersampling ideas.

It commonly uses Tomek Links plus another cleaning or selection method.

Simple meaning:

> It removes majority examples near the decision boundary and reduces unnecessary majority examples.

This is useful to know as an additional theory concept, but it is not central to the required Day 3 exercise.

---

## 21. Cost-Sensitive Learning

Cost-sensitive learning does not change the dataset.

Instead, it changes how the model treats mistakes.

In fraud detection, missing fraud is usually more expensive than wrongly flagging a normal transaction.

So we tell the model:

> Mistakes on fraud cases should receive a higher penalty.

This can be done using class weights.

---

## 22. `class_weight="balanced"`

`class_weight="balanced"` automatically gives higher weight to the minority class.

Simple meaning:

> The rarer the class, the higher its penalty weight.

Example:

```python
RandomForestClassifier(class_weight="balanced")
```

This helps the model pay more attention to fraud cases.

---

## 23. Manual Class Weights: `class_weight={0: 1, 1: 100}`

Manual class weights allow us to define our own cost ratio.

Example:

```python
RandomForestClassifier(class_weight={0: 1, 1: 100})
```

Meaning:

```text
Normal class weight = 1
Fraud class weight  = 100
```

Simple interpretation:

> A fraud mistake is treated as 100 times more serious than a normal-class mistake.

This may increase recall, but it may also increase false positives.

That is why we compare:

- Precision
- Recall
- F1-score

especially for the minority class.

---

## 24. Random Forest

Random Forest is an ensemble model made of many decision trees.

Simple meaning:

> Many trees vote together to make the final prediction.

Why it is useful here:

- Strong baseline for tabular data
- Handles non-linear relationships
- Works well without heavy preprocessing
- Supports `class_weight`

In this exercise, Random Forest is used to compare different imbalance-handling strategies.

---

## 25. XGBoost

XGBoost is a boosting algorithm based on decision trees.

Simple meaning:

> XGBoost builds trees one after another, and each new tree focuses on correcting previous mistakes.

Why it is useful:

- Very strong for tabular data
- Often performs well in Kaggle-style problems
- Has imbalance handling through `scale_pos_weight`

In the expert task, we combine:

```text
SMOTE + XGBoost + scale_pos_weight
```

Then we compare it with the best previous model.

---

## 26. `scale_pos_weight`

`scale_pos_weight` is XGBoost's class imbalance parameter.

A common starting value is:

```text
Number of negative examples / Number of positive examples
```

For the full Credit Card Fraud dataset:

```text
284,315 / 492 ≈ 577.88
```

So a possible starting value is around:

```text
scale_pos_weight ≈ 578
```

Simple meaning:

> XGBoost should pay much more attention to fraud cases.

Important warning:

If we use SMOTE and also use a very high `scale_pos_weight`, we may over-emphasise the minority class. This can increase false positives. Therefore, we compare results carefully.

---

## 27. Train/Test Split

Before training a model, we split the dataset into:

| Part | Purpose |
|---|---|
| Training set | Used to train the model |
| Test set | Used to evaluate the model on unseen data |

The test set must represent real unseen data.

---

## 28. Stratified Split

Because fraud is rare, we should use stratification.

Example:

```python
train_test_split(X, y, test_size=0.2, stratify=y, random_state=42)
```

Simple meaning:

> Keep the same fraud/non-fraud ratio in both training and test data.

Without stratification, the test set might contain too few fraud cases, making evaluation unstable.

---

## 29. Data Leakage

Data leakage happens when information from the test set accidentally enters the training process.

In imbalanced learning, the most common leakage mistake is:

```text
Applying SMOTE or oversampling before train/test split
```

Why this is wrong:

- Duplicate or synthetic examples may appear in both train and test sets.
- The model gets indirect access to test information.
- Evaluation becomes unrealistically good.

Correct order:

```text
1. Split data into train and test
2. Apply resampling only on training data
3. Train the model
4. Evaluate on untouched test data
```

This is one of the most important practical rules in the entire exercise.

---

## 30. Baseline Model

A baseline model is the first model we use for comparison.

In this exercise, the baseline is:

```text
RandomForestClassifier trained on untreated imbalanced data
```

Why it matters:

> We need a starting point to judge whether resampling, class weights, threshold tuning, or XGBoost actually improve the model.

---

## 31. Untreated Model

An untreated model is trained directly on the original imbalanced training data.

No oversampling, undersampling, SMOTE, Tomek Links, or class weights are applied.

This model shows how the algorithm behaves without imbalance correction.

---

## 32. Model Comparison Plan

For the intermediate part, we compare five Random Forest models:

1. Untreated data
2. Random Oversampling
3. SMOTE
4. Random Undersampling
5. Tomek Links

For each model, we compare:

- Accuracy
- F1-score
- ROC-AUC
- ROC curve

For the expert part, we compare:

1. Random Forest with `class_weight="balanced"`
2. Random Forest with `class_weight={0: 1, 1: 100}`
3. Threshold-optimised model
4. SMOTE + XGBoost + `scale_pos_weight`

---

## 33. Real-Time Fraud Detection Considerations

The final question is not only about the best metric.

For real-time fraud detection, we must consider:

- Prediction speed
- Recall: how much fraud is caught
- Precision: how many alerts are truly fraud
- False positives: customer inconvenience
- False negatives: financial loss
- Model complexity
- Stability on new data
- Ease of deployment

A model with the highest AUC may not always be the best business model.

For example:

- Very high recall but very low precision may overwhelm fraud analysts.
- Very high precision but low recall may miss too much fraud.
- A very complex model may be difficult to deploy in real time.

The final recommendation should balance model performance and business usability.

---

## 34. Final Concept Summary

The central lesson of imbalanced data is:

> A model can look very accurate while failing on the class that matters most.

For credit card fraud detection:

- Accuracy alone is not enough.
- Fraud is the minority class and positive class.
- Recall tells us how much fraud we catch.
- Precision tells us how reliable fraud alerts are.
- F1-score balances precision and recall.
- ROC-AUC shows overall separation ability.
- PR-AUC can be useful for rare-event problems.
- Resampling changes the training data.
- Class weighting changes the cost of mistakes.
- Threshold optimisation changes the final decision rule.
- SMOTE creates synthetic minority examples.
- Tomek Links clean the class boundary.
- XGBoost uses `scale_pos_weight` to handle imbalance.
- Resampling must happen only after train/test split and only on training data.

---

## 35. Interview-Style Explanation

If asked in an interview, explain it like this:

> Imbalanced data occurs when one class is much rarer than the other, such as fraud transactions in credit card data. In such cases, accuracy can be misleading because a model can predict every transaction as normal and still achieve very high accuracy while catching no fraud. Therefore, I would evaluate the model using precision, recall, F1-score, ROC-AUC, and possibly PR-AUC. To handle imbalance, I would compare resampling methods such as Random Oversampling, SMOTE, Random Undersampling, and Tomek Links, as well as cost-sensitive learning using class weights. I would make sure to apply resampling only on the training data to avoid data leakage. Finally, I would tune the decision threshold based on the business cost of false positives and false negatives.

---

## 36. Day 3 Practical Checklist

Use this checklist while solving the notebook.

### Beginner

- [ ] Load `creditcard.csv`
- [ ] Check shape and basic structure
- [ ] Identify features and target
- [ ] Calculate class distribution
- [ ] Calculate class percentages
- [ ] Create count plot with absolute counts
- [ ] Explain why high accuracy can still be bad

### Intermediate

- [ ] Split data into train and test using `stratify=y`
- [ ] Apply Random Oversampling on training data only
- [ ] Apply SMOTE on training data only
- [ ] Apply Random Undersampling on training data only
- [ ] Apply Tomek Links on training data only
- [ ] Print new class distribution after each method
- [ ] Create `evaluate_model()` function
- [ ] Train Random Forest on all five variants
- [ ] Compare Accuracy, F1-score, and ROC-AUC
- [ ] Plot ROC curves for all five models
- [ ] Identify best AUC model

### Expert

- [ ] Train Random Forest with `class_weight="balanced"`
- [ ] Train Random Forest with `class_weight={0: 1, 1: 100}`
- [ ] Compare minority-class precision, recall, and F1-score
- [ ] Implement threshold optimisation from 0.10 to 0.90
- [ ] Plot threshold vs F1-score
- [ ] Mark the best threshold
- [ ] Train SMOTE + XGBoost + `scale_pos_weight`
- [ ] Compare with the best previous model
- [ ] Decide which model is suitable for real-time fraud detection

---

## 37. Recommended Final Interpretation Structure

At the end of the exercise, write the conclusion using this structure:

1. **Class imbalance severity**  
   State how rare fraud is in the dataset.

2. **Why accuracy is insufficient**  
   Explain why a high accuracy model can still miss fraud.

3. **Best resampling method**  
   Compare Random Oversampling, SMOTE, Random Undersampling, and Tomek Links.

4. **Best cost-sensitive method**  
   Compare `class_weight="balanced"` and manual weights.

5. **Best threshold**  
   Explain how threshold tuning changed F1, precision, and recall.

6. **XGBoost comparison**  
   Explain whether SMOTE + XGBoost + `scale_pos_weight` improved performance.

7. **Business recommendation**  
   Recommend the most suitable approach for real-time fraud detection.

---

## Source Notes

This theory note is based on:

- educx Module 2 Machine Learning — Learning Day 3: Imbalanced Data
- Instructor material on imbalanced data, metrics, SMOTE, Tomek Links, NearMiss, class weighting, and ROC-AUC
- Credit Card Fraud dataset used in the Day 3 practical exercise
