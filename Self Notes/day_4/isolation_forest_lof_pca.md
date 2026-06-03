# Notebook 2 Summary — Intermediate Outlier Detection

## Project Context

This notebook continued **Learning Day 4: Outlier Detection** after completing the Beginner Z-Score notebook.

The goal of this notebook was to move from simple statistical outlier detection to **model-based outlier detection**.

We worked with the **Industrial Equipment Monitoring Dataset** and used the following sensor columns:

- `temperature`
- `pressure`
- `vibration`
- `humidity`

Each row represents one machine observation, also called one **data point**.

---

## Step 1 — Loaded the Dataset

We loaded the equipment monitoring dataset from:

```python
equipment_anomaly_data.csv
```

The dataset contained:

- **7,672 rows**
- **7 columns**

Selected sensor columns:

- `temperature`
- `pressure`
- `vibration`
- `humidity`

The column `faulty` was not used for unsupervised model training because it is the label/answer column.

---

## Step 2 — Prepared and Scaled Sensor Features

We created two feature datasets:

```python
X
X_scaled
```

Where:

- `X` contains the original sensor values
- `X_scaled` contains standardized sensor values

Scaling was done using:

```python
StandardScaler()
```

Scaling transforms each sensor column so that it has approximately:

- mean = `0`
- standard deviation = `1`

This step is important because **Local Outlier Factor** uses distance-based comparisons.  
Without scaling, columns with larger numeric values could dominate the distance calculation.

---

## Step 3 — Trained Isolation Forest

We trained an **Isolation Forest** model using the scaled sensor features.

Model setting:

```python
contamination = 0.05
```

This means the model was expected to flag around **5%** of rows as outliers.

Isolation Forest result:

| Metric | Value |
|---|---:|
| Total rows | 7,672 |
| Isolation Forest outliers | 384 |
| Outlier percentage | 5.01% |

Isolation Forest detects rows that are easier to isolate using random splits.

Simple interpretation:

> If a row is very different from the rest, the model can separate it quickly, so it may be an outlier.

---

## Step 3B — Built Isolation Forest Detection Summary Chart

We created a donut chart showing:

- normal rows
- Isolation Forest outlier rows

Result:

| Row Type | Rows | Percentage |
|---|---:|---:|
| Normal rows | 7,288 | 94.99% |
| Outlier rows | 384 | 5.01% |

The chart confirmed that the model output matched the `contamination = 0.05` setting.

---

## Step 4 — Trained Local Outlier Factor

We trained a **Local Outlier Factor (LOF)** model using the scaled sensor features.

Model setting:

```python
contamination = 0.05
```

LOF result:

| Metric | Value |
|---|---:|
| Total rows | 7,672 |
| LOF outliers | 384 |
| Outlier percentage | 5.01% |

LOF detects rows that are locally unusual compared to their nearby neighbors.

Simple interpretation:

> LOF asks whether a row is lonely or unusual compared to nearby rows.

---

## Step 5 — Compared Isolation Forest and LOF Outlier Counts

Both models detected the same number of outliers:

| Method | Outlier Rows | Outlier Percentage |
|---|---:|---:|
| Isolation Forest | 384 | 5.01% |
| Local Outlier Factor | 384 | 5.01% |

This happened because both models used:

```python
contamination = 0.05
```

However, detecting the same number of outliers does not mean both models detected the same rows.

---

## Step 6 — Calculated the Jaccard Coefficient

To compare row-level agreement between Isolation Forest and LOF, we calculated the **Jaccard coefficient**.

Jaccard formula:

```text
Jaccard = size of intersection / size of union
```

Where:

- intersection = rows detected by both methods
- union = rows detected by at least one method

Results:

| Metric | Value |
|---|---:|
| Isolation Forest outliers | 384 |
| LOF outliers | 384 |
| Shared outliers | 32 |
| Total unique outliers across both methods | 736 |
| Jaccard coefficient | 0.0435 |

Interpretation:

The Jaccard coefficient was very low.

This means Isolation Forest and LOF detected mostly different outlier rows.

---

## Step 7 — Created Method Agreement Categories

We created a new column:

```python
method_agreement
```

This grouped rows into four categories:

- `Normal by both`
- `Isolation Forest only`
- `LOF only`
- `Both methods`

Agreement results:

| Category | Rows | Percentage |
|---|---:|---:|
| Normal by both | 6,936 | 90.41% |
| Isolation Forest only | 352 | 4.59% |
| LOF only | 352 | 4.59% |
| Both methods | 32 | 0.42% |

Main insight:

Only **32 rows** were detected as outliers by both methods.

These shared outliers may deserve higher investigation priority because two different algorithms agreed that they are unusual.

---

## Step 7B — Built Agreement Chart

We created a horizontal bar chart to show:

- rows normal by both models
- rows detected only by Isolation Forest
- rows detected only by LOF
- rows detected by both methods

The chart confirmed visually that the two models had very low overlap.

---

## Step 8 — Applied PCA for 2D Visualization

We used **Principal Component Analysis (PCA)** to reduce the four sensor columns into two components:

- `PC1`
- `PC2`

PCA explained variance:

| Component | Explained Variance |
|---|---:|
| PC1 | 28.20% |
| PC2 | 25.22% |
| PC1 + PC2 | 53.41% |

This means the 2D PCA plot captured around **53.41%** of the sensor variation.

Important note:

PCA was used for visualization only.  
It does not show 100% of the original sensor information.

---

## Step 9 — Built PCA Scatter Plot

We created a PCA scatter plot showing method agreement categories.

Color groups:

- grey = normal by both methods
- blue = Isolation Forest only
- orange = LOF only
- green = both methods

Main insights:

- Normal rows formed a dense central region.
- Isolation Forest and LOF outliers appeared in different areas of the PCA space.
- Only a small number of green points appeared, confirming the low Jaccard score.
- The two methods are detecting different types of unusual sensor behavior.

---

## Key Business Interpretation

Isolation Forest and LOF both detected around 5% of rows as outliers, but they did not agree strongly on which rows were outliers.

This shows that outlier detection depends heavily on the algorithm used.

From a machine monitoring perspective:

- rows detected by both methods should be prioritized for inspection
- rows detected by only one method should still be reviewed because each method captures a different type of unusual behavior
- outlier detection should be used as an investigation tool, not an automatic deletion rule

---

## Methods Completed in This Notebook

Completed:

- Dataset loading
- Feature scaling
- Isolation Forest
- Isolation Forest summary chart
- Local Outlier Factor
- Model count comparison
- Jaccard coefficient
- Method agreement chart
- PCA transformation
- PCA agreement scatter plot

---

## Next Notebook Plan

In the next notebook, we will continue with extended outlier detection methods from the uploaded theory/code material:

1. **ABOD — Angle-Based Outlier Detection**
2. **CBLOF — Cluster-Based Local Outlier Factor**
3. **LoOP — Local Outlier Probability**

After that, we will continue to the Expert section:

1. KDD Cup 1999 dataset
2. Autoencoder anomaly detection
3. Reconstruction error
4. 95th percentile threshold
5. Precision, Recall, and F1-Score
6. Autoencoder vs Isolation Forest comparison
