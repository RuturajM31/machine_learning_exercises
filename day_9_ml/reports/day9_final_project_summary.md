# Learning Day 9 — Final Project Summary

## Project Topic

Ensemble Methods: Bagging, Random Forest, Stacking, Blending, Three-Layer Stacking, and Gradient Boosting.

## Business Use Case

Predict whether a bank customer will subscribe to a term deposit.

## Recommended Model

StackingClassifier with Random Forest meta-model.

## Reason

This model achieved the best test F1-score and the highest recall among the final compared models.

## Key Final Results

- Best F1 model: StackingClassifier (RF meta) with Test F1 = 0.8597
- Best recall model: StackingClassifier (RF meta) with Test Recall = 0.9064
- Best ROC-AUC model: StackingClassifier (LR meta) with Test ROC-AUC = 0.9265
- Best accuracy model: Three-Layer Stacking with Test Accuracy = 0.8612

## Main Learning

A more complex model is not always the best practical model.
Three-Layer Stacking worked well, but it did not beat the simpler RF-meta StackingClassifier by F1-score.
Manual OOF Stacking was important for understanding how stacking works internally.

## MVD Status

All Beginner, Intermediate, and Expert MVD tasks were completed.