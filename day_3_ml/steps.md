Project Flow — Imbalanced Fraud Detection
Simple End-to-End Workflow

1. Understand the business problem
Fraud transactions are extremely rare, so accuracy alone can be misleading.

2. Load the dataset
Loaded the Credit Card Fraud dataset and used a local CSV fallback when KaggleHub failed.

3. Inspect the data
Checked dataset shape, column names, data types, missing values, and duplicates.

4. Analyse class imbalance
Confirmed that fraud cases make up only around 0.17% of all transactions.

5. Build a dummy baseline
Showed that predicting every transaction as normal gives high accuracy but misses all fraud.

6. Split the data correctly
Used stratified train/test split so both sets kept the same fraud ratio.

7. Scale selected features
Scaled only Time and Amount using RobustScaler.

8. Apply resampling methods on training data only
Compared Random Oversampling, SMOTE, Random Undersampling, and Tomek Links.

9. Train Random Forest models
Trained one Random Forest model for each training-data version.

10. Evaluate all models on the same test set
Compared Accuracy, Precision, Recall, F1-Score, and ROC-AUC fairly.

11. Plot ROC curves
Compared model separation ability and showed that ROC-AUC alone is not enough.

12. Test cost-sensitive learning
Trained Random Forest models with class_weight="balanced" and class_weight={0:1, 1:100}.

13. Optimise the decision threshold
Tested thresholds from 0.10 to 0.90 and found the best F1-Score at 0.40.

14. Train SMOTE + XGBoost
Tested an advanced model using SMOTE-balanced data and scale_pos_weight=1.0.

15. Compare final candidates
Compared Tomek RF at threshold 0.50, Tomek RF at threshold 0.40, and SMOTE + XGBoost.

16. Select the final practical model
Chose Tomek Links Random Forest with threshold 0.40 as the best practical model.

Final Takeaway

The best model was not simply the one with the highest ROC-AUC.

SMOTE + XGBoost had the highest ROC-AUC, but it created too many false alerts.

Tomek Links Random Forest with threshold 0.40 gave the best practical balance:

strong fraud detection,
high Precision,
best F1-Score,
very low false alerts,
and better real-time usability.