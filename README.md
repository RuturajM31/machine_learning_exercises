# Machine Learning Module 2 Portfolio

> A complete hands-on Machine Learning portfolio based on the **educx Module 2 Machine Learning Exercise Collection**: 15 learning days, 3 skill levels, and 45 structured exercise sets.

![Module](https://img.shields.io/badge/Module-2%20Machine%20Learning-0f172a?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Completed-16a34a?style=for-the-badge)
![Level](https://img.shields.io/badge/Levels-Beginner%20%7C%20Intermediate%20%7C%20Expert-2563eb?style=for-the-badge)
![Focus](https://img.shields.io/badge/Focus-Portfolio%20%7C%20MVD%20%7C%20BI%20Interpretation-7c3aed?style=for-the-badge)

---

## Table of Contents

- [About This Repository](#about-this-repository)
- [Repository Purpose](#repository-purpose)
- [What Makes This Portfolio Different](#what-makes-this-portfolio-different)
- [Official MVD Scope](#official-mvd-scope)
- [15-Day Learning Path](#15-day-learning-path)
- [Detailed Day-by-Day Coverage](#detailed-day-by-day-coverage)
- [Extra Work Beyond the MVD](#extra-work-beyond-the-mvd)
- [Professional Skills Demonstrated](#professional-skills-demonstrated)
- [Tools and Libraries](#tools-and-libraries)
- [Repository Structure](#repository-structure)
- [How to Read This Repository](#how-to-read-this-repository)
- [Selected Portfolio Highlights](#selected-portfolio-highlights)
- [Current Completion Status](#current-completion-status)
- [Future Deep-Dive Plan](#future-deep-dive-plan)

---

## About This Repository

This repository contains my complete hands-on work for **Module 2: Machine Learning** from **educx**.

It is not only a folder of notebooks. It is a structured learning portfolio that documents how I studied, implemented, evaluated, interpreted, and extended core Machine Learning topics across the full 15-day module.

The work follows the official MVD exercise structure and adds professional extensions such as:

- clean notebook documentation,
- business interpretation,
- BI-ready charts,
- source coverage checks,
- model comparison tables,
- explainability notes,
- fairness analysis,
- deployment thinking,
- final PDF documentation,
- and project-style summaries.

The goal is to show practical Machine Learning ability in a way that is useful for a **Data Analyst, BI Analyst, Data Scientist, or ML-focused Analytics role**.

---

## Repository Purpose

The main purpose of this repository is to document a complete applied Machine Learning learning journey.

The repository demonstrates that I can:

1. understand ML theory,
2. convert theory into working Python code,
3. evaluate models correctly,
4. explain model outputs in business language,
5. identify limitations and risks,
6. create clean and reproducible notebooks,
7. document work professionally,
8. and connect ML results to real analytics decisions.

Each learning day focuses on a specific Machine Learning topic and moves from beginner-level implementation to expert-level reflection.

---

## What Makes This Portfolio Different

Many learning repositories only show code. This repository goes further.

### 1. Theory-to-practice flow

Each major topic is handled through a learning flow:

```text
Concept → Dataset → Implementation → Metric → Chart → Interpretation → Business Meaning
```

### 2. Result-based conclusions

Notebook conclusions are not generic. They explain actual model outputs, metrics, comparisons, and practical meaning.

Examples:

- why one model performed better than another,
- what AUC or RMSE means in context,
- how false positives and false negatives affect a business case,
- why fairness metrics matter,
- and why AutoML still needs human judgement.

### 3. BI-ready presentation style

The notebooks and documentation are designed to be readable for both technical and business audiences.

Focus areas include:

- clean tables,
- executive-style visual summaries,
- readable chart titles,
- clear metric explanations,
- and business recommendations after technical results.

### 4. MVD plus extra learning

The official MVD tasks are treated as the minimum requirement. Additional work was added where useful, especially around:

- source coverage,
- PyCaret workflow automation,
- SHAP explainability,
- fairness analysis,
- transfer learning theory,
- deployment concepts,
- and professional reporting.

---

## Official MVD Scope

The uploaded educx MVD document defines the official Module 2 structure as:

| Scope Item | Description |
|---|---|
| Module | Machine Learning |
| Duration | 15 Learning Days |
| Skill Levels | Beginner, Intermediate, Expert |
| Total Exercise Sets | 45 exercise sets |
| Main Goal | Learn ML concepts through practical implementation, comparison, evaluation, and critical reflection |

### Skill level meaning

| Level | Focus |
|---|---|
| Beginner | Understand the concept and implement a first working example |
| Intermediate | Apply, compare, evaluate, and improve methods |
| Expert | Optimise, explain, reflect critically, and connect methods to real-world limitations |

---

## 15-Day Learning Path

| Day | Main Topic | Core Learning Goal |
|---:|---|---|
| 1 | Introduction to Machine Learning | Understand ML paradigms and build first supervised models |
| 2 | Preprocessing, Encoders, and Scalers | Prepare raw data correctly and avoid data leakage |
| 3 | Imbalanced Data | Handle rare-class problems and evaluate beyond accuracy |
| 4 | Outlier Detection | Detect unusual records with statistical and ML-based methods |
| 5 | Dimensionality Reduction with PCA | Reduce high-dimensional data for visualization and faster modelling |
| 6 | Autoencoders | Learn compressed representations and reconstruction-based anomaly concepts |
| 7 | Decision Trees | Build interpretable tree models and control overfitting |
| 8 | Clustering | Segment data using unsupervised learning methods |
| 9 | Ensemble Methods | Combine models using bagging, stacking, and blending ideas |
| 10 | Boosting | Use powerful boosting models such as XGBoost, CatBoost, and LightGBM |
| 11 | Hyperparameter Tuning | Search for strong model parameters using systematic and Bayesian methods |
| 12 | Linear and Logistic Regression | Build interpretable regression and classification models |
| 13 | Reinforcement Learning | Understand agents, rewards, Q-Learning, and DQN concepts |
| 14 | Transfer Learning and Pre-trained Models | Reuse pre-trained deep learning models for new tasks |
| 15 | AutoML with PyCaret | Automate ML workflows while understanding explainability, fairness, and deployment |

---

## Detailed Day-by-Day Coverage

The following section summarizes the full 15-day MVD coverage and the practical skills demonstrated.

---

### Day 1 — Introduction to Machine Learning

**Main idea:** Machine Learning algorithms learn patterns from data instead of being explicitly programmed for every rule.

| Level | Official Focus | Practical Skills Demonstrated |
|---|---|---|
| Beginner | Classifying ML paradigms | Identified supervised, unsupervised, and reinforcement learning problems using examples such as spam detection, customer segmentation, and chess-playing agents |
| Intermediate | Data exploration and first metrics | Loaded datasets, inspected missing values, calculated survival rates, trained Logistic Regression, and interpreted classification reports |
| Expert | Bias-variance tradeoff and learning curves | Compared Decision Tree depths, plotted learning curves, diagnosed overfitting and underfitting, and used bootstrap-style thinking for bias and variance |

**Key concepts covered:**

- supervised learning,
- unsupervised learning,
- reinforcement learning,
- train/test split,
- first classification metrics,
- bias and variance,
- learning curves.

---

### Day 2 — Preprocessing, Encoders, and Scalers

**Main idea:** Raw data is rarely model-ready. Features must be cleaned, encoded, scaled, and transformed without causing data leakage.

| Level | Official Focus | Practical Skills Demonstrated |
|---|---|---|
| Beginner | LabelEncoder and OneHotEncoder | Encoded categorical variables and explained why nominal features should not be treated as ordered values |
| Intermediate | Pipeline with ColumnTransformer | Built preprocessing pipelines using `ColumnTransformer`, `StandardScaler`, `OneHotEncoder`, and model pipelines |
| Expert | Custom Transformer and feature engineering | Created custom feature logic inside a pipeline and discussed target encoding leakage risk |

**Key concepts covered:**

- categorical encoding,
- numerical scaling,
- `Pipeline`,
- `ColumnTransformer`,
- leakage prevention,
- custom transformers,
- feature engineering.

---

### Day 3 — Imbalanced Data

**Main idea:** In real datasets, the important class is often rare. Accuracy can look high while the model completely misses critical cases.

| Level | Official Focus | Practical Skills Demonstrated |
|---|---|---|
| Beginner | Identifying and visualising class distribution | Calculated class ratios and visualized imbalance using count plots and annotations |
| Intermediate | Oversampling and undersampling | Compared Random Oversampling, SMOTE, Random Undersampling, Tomek Links, and untreated data |
| Expert | Cost-sensitive learning and threshold optimisation | Used class weights, threshold tuning, and compared Precision, Recall, F1, and AUC for rare-class detection |

**Key concepts covered:**

- class imbalance,
- minority class detection,
- SMOTE,
- Tomek Links,
- class weights,
- ROC curves,
- threshold optimization,
- Precision/Recall tradeoff.

---

### Day 4 — Outlier Detection

**Main idea:** Outliers can be noise, measurement errors, fraud attempts, or rare but meaningful events.

| Level | Official Focus | Practical Skills Demonstrated |
|---|---|---|
| Beginner | Statistical outlier detection | Used Z-scores, boxplots, and before/after statistics after removing outliers |
| Intermediate | Isolation Forest and Local Outlier Factor | Detected anomalies in high-dimensional data and compared methods using PCA visualization and overlap logic |
| Expert | Autoencoder anomaly detection | Used reconstruction error logic to identify unusual records and compared deep learning anomaly detection with Isolation Forest |

**Key concepts covered:**

- Z-score,
- boxplots,
- Isolation Forest,
- Local Outlier Factor,
- reconstruction error,
- anomaly thresholds,
- real-time anomaly detection tradeoffs.

---

### Day 5 — Dimensionality Reduction with PCA

**Main idea:** High-dimensional data can become difficult to model and visualize. PCA compresses features while preserving important variance.

| Level | Official Focus | Practical Skills Demonstrated |
|---|---|---|
| Beginner | PCA for visualization | Standardized data, applied PCA to 2D and 3D, and visualized class separation |
| Intermediate | Optimal components and scree plot | Used cumulative explained variance and scree plots to choose the number of components |
| Expert | PCA vs UMAP vs t-SNE | Compared linear and non-linear dimensionality reduction methods using runtime and trustworthiness concepts |

**Key concepts covered:**

- PCA,
- explained variance,
- scree plot,
- dimensionality reduction,
- t-SNE,
- UMAP,
- trustworthiness score,
- visualization of high-dimensional data.

---

### Day 6 — Autoencoders

**Main idea:** Autoencoders learn to reconstruct their input through a compressed bottleneck representation.

| Level | Official Focus | Practical Skills Demonstrated |
|---|---|---|
| Beginner | Simple dense autoencoder | Built encoder-decoder architecture for MNIST-style reconstruction |
| Intermediate | Convolutional autoencoder | Used convolutional layers for image reconstruction and compared dense vs convolutional reconstruction quality |
| Expert | Variational Autoencoder | Studied latent distributions, reparameterization trick, KL divergence, and generative sampling ideas |

**Key concepts covered:**

- encoder,
- decoder,
- bottleneck,
- reconstruction loss,
- convolutional autoencoder,
- VAE,
- latent space,
- KL divergence.

---

### Day 7 — Decision Trees

**Main idea:** Decision Trees create interpretable yes/no decision paths but can easily overfit without pruning.

| Level | Official Focus | Practical Skills Demonstrated |
|---|---|---|
| Beginner | First Decision Tree | Trained `DecisionTreeClassifier`, visualized the tree, identified the root feature, and compared Gini vs Entropy |
| Intermediate | Pruning and feature importance | Tested `min_samples_leaf`, cost-complexity pruning, and feature importance interpretation |
| Expert | Oblique trees and SHAP | Explored advanced tree explainability, SHAP concepts, and practical limitations of unavailable/unstable packages |

**Key concepts covered:**

- Decision Trees,
- Gini impurity,
- Entropy,
- tree depth,
- leaf nodes,
- pruning,
- `ccp_alpha`,
- feature importance,
- SHAP explanation.

---

### Day 8 — Clustering

**Main idea:** Clustering finds groups in unlabeled data. Different algorithms define “groups” differently.

| Level | Official Focus | Practical Skills Demonstrated |
|---|---|---|
| Beginner | K-Means customer segmentation | Applied K-Means with multiple k values, visualized clusters, and used the elbow curve |
| Intermediate | DBSCAN and Silhouette | Built RFM-style customer features, scaled data, tested DBSCAN grids, and compared clustering quality |
| Expert | Hierarchical clustering and Gap Statistic | Created dendrograms, implemented Gap Statistic logic, and compared clustering methods using multiple metrics |

**Key concepts covered:**

- unsupervised learning,
- K-Means,
- centroids,
- inertia,
- elbow method,
- DBSCAN,
- noise points,
- Silhouette score,
- RFM segmentation,
- hierarchical clustering,
- dendrogram,
- Gap Statistic,
- Davies-Bouldin,
- Calinski-Harabasz.

**Additional work beyond MVD:**

The clustering work was expanded beyond only K-Means and DBSCAN. Extra coverage included methods such as K-Modes, K-Medoids, MiniBatchKMeans, OPTICS, BIRCH, Gaussian Mixture Models, density/grid-style clustering concepts, and constraint-style clustering explanations where relevant.

---

### Day 9 — Ensemble Methods

**Main idea:** Ensemble models combine multiple learners to improve stability, accuracy, or robustness.

| Level | Official Focus | Practical Skills Demonstrated |
|---|---|---|
| Beginner | Random Forest vs single tree | Compared single Decision Tree and Random Forest models, feature importance, and estimator counts |
| Intermediate | StackingClassifier | Built stacking models with multiple base learners and compared them against individual models |
| Expert | Out-of-fold predictions and blending | Implemented manual OOF stacking, blending logic, and discussed whether additional complexity is justified |

**Key concepts covered:**

- Bagging,
- Random Forest,
- estimator count,
- stacking,
- meta-model,
- model diversity,
- out-of-fold predictions,
- blending,
- leakage prevention in stacking.

---

### Day 10 — Boosting

**Main idea:** Boosting trains models sequentially so each new model focuses on previous errors.

| Level | Official Focus | Practical Skills Demonstrated |
|---|---|---|
| Beginner | First XGBoost classifier | Trained XGBoost, compared with Random Forest, and interpreted feature importance |
| Intermediate | Hyperparameter tuning with GridSearch | Tuned boosting models, compared XGBoost and CatBoost, and used early stopping logic |
| Expert | LightGBM and Optuna | Used Bayesian-style optimization concepts and compared boosted model ensembles |

**Key concepts covered:**

- boosting,
- gradient boosting,
- XGBoost,
- CatBoost,
- LightGBM,
- learning rate,
- tree depth,
- early stopping,
- Optuna,
- parameter importance,
- ensemble averaging.

---

### Day 11 — Hyperparameter Tuning

**Main idea:** Hyperparameter tuning systematically searches for better model settings.

| Level | Official Focus | Practical Skills Demonstrated |
|---|---|---|
| Beginner | GridSearchCV and RandomizedSearchCV | Compared exhaustive and random search strategies, runtime, and best scores |
| Intermediate | Bayesian optimisation | Studied Bayesian search, convergence, exploration vs exploitation, and acquisition functions |
| Expert | Neural Architecture Search light | Explored KerasTuner, Hyperband, neural architecture tuning, and resource-aware search |

**Key concepts covered:**

- hyperparameters,
- GridSearchCV,
- RandomizedSearchCV,
- nested cross-validation,
- Bayesian optimization,
- scikit-optimize concepts,
- Optuna,
- KerasTuner,
- Hyperband,
- Successive Halving,
- NAS concepts.

**Additional work beyond MVD:**

Day 11 included extended source coverage and professional documentation such as master theory notes, notebook QA, method flow, business interpretation, and BI-style presentation material.

---

### Day 12 — Linear and Logistic Regression

**Main idea:** Regression models remain essential because they are interpretable, fast, and strong baselines for many business tasks.

| Level | Official Focus | Practical Skills Demonstrated |
|---|---|---|
| Beginner | Linear Regression first steps | Built simple and multiple linear regression models, interpreted coefficients, intercept, MSE, and R² |
| Intermediate | Ridge, Lasso, ElasticNet | Compared regularization methods, alpha values, coefficient shrinkage, and feature selection behavior |
| Expert | GLMs and Poisson Regression | Compared linear regression, Poisson regression, and Negative Binomial regression for count-data problems |

**Key concepts covered:**

- simple linear regression,
- multiple linear regression,
- coefficients,
- intercept,
- MSE,
- RMSE,
- MAE,
- R²,
- Ridge,
- Lasso,
- ElasticNet,
- LassoCV,
- GLMs,
- Poisson regression,
- Negative Binomial regression,
- logistic regression,
- classification metrics.

---

### Day 13 — Reinforcement Learning

**Main idea:** Reinforcement Learning trains an agent through actions, rewards, and interaction with an environment.

| Level | Official Focus | Practical Skills Demonstrated |
|---|---|---|
| Beginner | Exploring a Gym environment | Used CartPole-style environments, observations, actions, rewards, done flags, and heuristic policies |
| Intermediate | Q-Learning on FrozenLake | Implemented Q-Learning, epsilon-greedy exploration, alpha/gamma experiments, and deterministic vs slippery environments |
| Expert | Deep Q-Network with PyTorch | Studied DQN architecture, replay buffer, target network, DDQN idea, and reward-curve interpretation |

**Key concepts covered:**

- agent,
- environment,
- state,
- action,
- reward,
- episode,
- policy,
- Q-table,
- alpha,
- gamma,
- epsilon-greedy,
- stochastic transitions,
- DQN,
- replay buffer,
- target network,
- Double DQN.

**Additional work beyond MVD:**

Day 13 included a detailed master theory document and cell-by-cell summary documentation for clearer long-term learning.

---

### Day 14 — Transfer Learning and Pre-trained Models

**Main idea:** Transfer Learning reuses knowledge from models trained on large datasets and adapts it to smaller or domain-specific datasets.

| Level | Official Focus | Practical Skills Demonstrated |
|---|---|---|
| Beginner | Feature extraction with a pre-trained model | Used MobileNetV2-style feature extraction, frozen base layers, pooling, classification heads, and confusion matrices |
| Intermediate | Fine-tuning | Studied EfficientNet-style fine-tuning, learning-rate control, layer unfreezing, and Grad-CAM explanation |
| Expert | Domain adaptation and few-shot learning | Covered few-shot learning, data augmentation, MixUp, and prototypical classifier logic |

**Key concepts covered:**

- pre-trained models,
- transfer learning,
- feature extraction,
- frozen base model,
- classification head,
- fine-tuning,
- learning-rate scheduling,
- Grad-CAM,
- domain adaptation,
- few-shot learning,
- MixUp,
- prototypical networks.

**Additional work beyond MVD:**

Day 14 included an extensive master theory PDF covering transfer learning strategies, decision rules, training phases, NLP transfer ideas, Grad-CAM, MixUp, few-shot learning, and model-selection guidance.

---

### Day 15 — AutoML with PyCaret

**Main idea:** AutoML accelerates repetitive ML workflows, but it does not remove the need for human judgement, fairness review, explainability, and deployment monitoring.

| Level | Official Focus | Practical Skills Demonstrated |
|---|---|---|
| Beginner | PyCaret setup and model comparison | Used PyCaret `setup()`, `compare_models()`, `create_model()`, `evaluate_model()`, confusion matrix, and AUC curve |
| Intermediate | Tuning, blending, and deployment | Tuned top models with `tune_model()`, created blended models, compared AUC/Precision/Recall, and saved/loaded pipelines |
| Expert | AutoML limits and fairness analysis | Used SHAP-style interpretation, fairness metrics, Fairlearn mitigation concepts, and fairness-performance tradeoff analysis |

**Key concepts covered:**

- AutoML,
- PyCaret,
- `setup()`,
- `compare_models()`,
- `create_model()`,
- `tune_model()`,
- `blend_models()`,
- `evaluate_model()`,
- `plot_model()`,
- `predict_model()`,
- `pull()`,
- `finalize_model()`,
- `save_model()`,
- `load_model()`,
- SHAP,
- demographic parity,
- equalized odds,
- Fairlearn,
- ExponentiatedGradient,
- fairness-performance tradeoff,
- REST API deployment idea.

**Additional work beyond MVD:**

Day 15 was expanded with:

- PyCaret workflow automation coverage,
- PyCaret module comparison,
- version compatibility notes,
- AutoML tool comparison,
- production risks,
- EDA and preprocessing notes,
- command reference,
- master theory PDF,
- MVD professional summary PDF,
- and extra-source coverage notebook.

---

## Extra Work Beyond the MVD

The MVD was the required assignment structure. The work was extended to make the repository more professional and more useful as a portfolio.

### 1. Source audit and coverage mapping

For several topics, uploaded course files, scripts, notes, and assignment checklists were audited before final notebooks or documents were created.

This helped ensure that the work covered not only the exercise checklist but also the broader course material.

Examples:

- source inventory,
- missing-topic checks,
- topic-to-notebook mapping,
- coverage matrices,
- final source coverage checklists.

### 2. Professional notebook design

Notebook quality was improved across the module.

Standards used:

- clean introduction sections,
- HTML Markdown explanation blocks,
- small manageable code cells,
- comments explaining important logic,
- clear variable flow,
- result-based conclusion blocks,
- business interpretation after outputs,
- and local-safe execution logic.

### 3. BI-ready visual storytelling

Charts were treated as communication tools, not just code outputs.

The charting style focused on:

- meaningful titles,
- readable axes,
- sorted comparisons,
- metric annotations,
- business subtitles,
- clean spacing,
- and executive-ready visual summaries.

### 4. Business interpretation

Many notebooks include business-level interpretation, such as:

- which model should be selected,
- what metric matters most for the use case,
- how false positives and false negatives affect decisions,
- why model complexity may or may not be justified,
- and how a model result can support BI dashboards or operational workflows.

### 5. Explainability and fairness

The portfolio includes responsible ML themes that are important in real-world analytics.

Topics include:

- feature importance,
- SHAP interpretation,
- discriminatory feature risk,
- fairness metrics,
- demographic parity,
- equalized odds,
- fairness mitigation,
- and fairness-performance tradeoff.

### 6. Deployment and production thinking

The work goes beyond model training and includes deployment-oriented thinking.

Topics include:

- saving and loading models,
- reusing preprocessing pipelines,
- REST API concepts,
- version compatibility,
- model monitoring,
- data drift,
- model drift,
- and responsible use of AutoML.

### 7. Professional documentation package

Several learning days include additional PDFs and summaries.

Examples:

- Master Theory documents,
- MVD Assignment Summary documents,
- Notebook-by-Notebook summaries,
- Variable and Method Flow documents,
- Business Interpretation summaries,
- QA and Execution reports,
- Glossaries,
- and portfolio-style presentation documents.

---

## Professional Skills Demonstrated

This repository demonstrates both technical and analytical skills.

### Machine Learning skills

- supervised learning,
- unsupervised learning,
- reinforcement learning fundamentals,
- preprocessing,
- feature engineering,
- model training,
- model evaluation,
- model tuning,
- model comparison,
- model interpretation,
- model documentation.

### Data Analytics and BI skills

- exploratory data analysis,
- KPI-style metric interpretation,
- business-oriented model comparison,
- clean visual reporting,
- dashboard-thinking,
- explaining technical outputs to non-technical users.

### Responsible AI skills

- fairness checking,
- sensitive feature awareness,
- explainability,
- model limitation analysis,
- human review and governance thinking.

### Engineering and workflow skills

- Python notebook organization,
- reproducible workflows,
- pipeline usage,
- model saving/loading,
- version compatibility awareness,
- deployment-readiness thinking.

---

## Tools and Libraries

| Area | Tools and Libraries |
|---|---|
| Data handling | `pandas`, `numpy` |
| Visualization | `matplotlib`, `seaborn`, custom BI-style plots |
| Preprocessing | `StandardScaler`, `OneHotEncoder`, `LabelEncoder`, `ColumnTransformer`, `Pipeline` |
| Classical ML | `scikit-learn` |
| Imbalanced learning | `imbalanced-learn`, SMOTE, Tomek Links, class weighting |
| Tree models | Decision Trees, Random Forests, pruning, feature importance |
| Boosting | XGBoost, CatBoost, LightGBM |
| Tuning | GridSearchCV, RandomizedSearchCV, Bayesian search concepts, Optuna, KerasTuner concepts |
| Clustering | K-Means, DBSCAN, hierarchical clustering, GMM, clustering metrics |
| Deep Learning | TensorFlow/Keras concepts, PyTorch concepts where relevant |
| Autoencoders | Dense autoencoders, convolutional autoencoders, VAE concepts |
| Reinforcement Learning | Gymnasium concepts, Q-Learning, DQN/DDQN concepts |
| Transfer Learning | MobileNetV2, EfficientNet concepts, Grad-CAM, fine-tuning |
| AutoML | PyCaret |
| Explainability | SHAP, feature importance, Grad-CAM |
| Fairness | Fairlearn, demographic parity, equalized odds |
| Documentation | Markdown, HTML Markdown, PDF summaries, portfolio reporting |

---

## Repository Structure

The exact folder names may change as the portfolio is reorganized, but the repository generally follows this structure:

```text
ML Exercises/
│
├── README.md
│
├── day_01_ml/
├── day_02_ml/
├── day_03_ml/
├── day_04_ml/
├── day_05_ml/
├── day_06_ml/
├── day_07_ml/
├── day_08_ml/
├── day_09_ml/
├── day_10_ml/
├── day_11_ml/
├── day_12_ml/
├── day_13_ml/
├── day_14_ml/
├── day_15_ml/
│
├── Self Notes/
│   ├── day_01/
│   ├── day_02/
│   ├── ...
│   └── day_15/
│
├── reports/
│   ├── master_theory_documents/
│   ├── mvd_assignment_summaries/
│   ├── business_interpretation/
│   └── qa_reports/
│
└── outputs/
    ├── charts/
    ├── models/
    └── tables/
```

### Folder meaning

| Folder | Purpose |
|---|---|
| `day_xx_ml/` | Main notebooks and code for each learning day |
| `Self Notes/` | Personal notes, theory notes, and learning explanations |
| `reports/` | PDF summaries, final documents, and professional documentation |
| `outputs/charts/` | Saved visual outputs from notebooks |
| `outputs/models/` | Saved trained model files where applicable |
| `outputs/tables/` | Saved metric tables and comparison outputs |

---

## How to Read This Repository

A recommended reading order:

1. Start with the README to understand the full module scope.
2. Open each `day_xx_ml/` folder in order.
3. Read the notebook introduction before running code.
4. Run notebooks cell by cell.
5. Review metric tables and charts.
6. Read the result-based conclusion blocks after outputs.
7. Check the supporting PDF documents where available.
8. Compare the work against the MVD checklist.

This order helps connect theory, code, metrics, visuals, and business interpretation.

---

## Selected Portfolio Highlights

### Interpretable ML

Decision Trees, Linear Regression, Logistic Regression, Ridge, Lasso, and ElasticNet were used to build models that can be explained clearly.

### Model evaluation discipline

The repository uses multiple metrics instead of relying only on accuracy.

Examples:

- Accuracy,
- Precision,
- Recall,
- F1-score,
- AUC,
- RMSE,
- MAE,
- R²,
- Silhouette,
- Davies-Bouldin,
- Calinski-Harabasz,
- fairness metrics.

### Advanced model comparison

The portfolio includes comparisons between:

- single trees and Random Forests,
- Random Forest and XGBoost,
- Grid Search and Random Search,
- K-Means and DBSCAN,
- baseline and tuned models,
- individual and blended models,
- baseline and fairness-mitigated models.

### Responsible ML

The later work includes fairness and explainability, especially in the AutoML/PyCaret day.

This includes:

- SHAP-style interpretation,
- sensitive feature awareness,
- demographic parity,
- equalized odds,
- Fairlearn mitigation,
- and fairness-performance tradeoff analysis.

### AutoML with human judgement

Day 15 shows that AutoML is powerful for fast benchmarking, but it does not replace the analyst.

The work explains:

- what PyCaret automates,
- what PyCaret does not automate,
- why fairness must be checked manually,
- why deployment requires monitoring,
- and why business context still matters.

---

## Current Completion Status

| Area | Status |
|---|---|
| 15-day MVD learning path | Completed |
| Beginner tasks | Completed |
| Intermediate tasks | Completed |
| Expert tasks | Completed |
| Practical notebooks | Completed across module topics |
| Result-based conclusions | Added to key notebooks |
| Professional documentation | Added for selected days |
| AutoML/PyCaret final MVD | Completed |
| Extra source coverage | Added where required |
| Deep-dive revision plan | Planned for Days 12 to 15 |

---

## Future Deep-Dive Plan

After the urgent submission phase, the next planned phase is a deeper learning restart for:

```text
ML Module 2 Deep Dive — Days 12 to 15
```

Planned deep-dive topics:

| Day | Deep-Dive Focus |
|---:|---|
| 12 | Linear Regression, Regularized Regression, GLMs, Logistic Regression |
| 13 | Reinforcement Learning, Q-Learning, DQN, DDQN concepts |
| 14 | Transfer Learning, pre-trained models, fine-tuning, Grad-CAM, few-shot learning |
| 15 | AutoML with PyCaret, SHAP, Fairness, Deployment, AutoML limitations |

The goal of the deep-dive phase is not only to submit work, but to understand the theory properly from scratch and connect it to practical analytics and business use cases.

---

## Final Note

This repository represents a complete Machine Learning learning portfolio. It combines structured course tasks, practical notebooks, professional documentation, BI-ready interpretation, and responsible ML thinking.

The main value of this work is not only that models were trained, but that results were explained, compared, questioned, and connected to real-world decision-making.
