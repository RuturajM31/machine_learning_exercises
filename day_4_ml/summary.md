# Final Summary — Outlier Detection Algorithms on Industrial Equipment Data

## Project Goal

The goal of this section was to detect unusual machine sensor readings using different outlier detection algorithms.

We used the Industrial Equipment Monitoring dataset.

Each row represents one machine observation.

The sensor columns used were:

- `temperature`
- `pressure`
- `vibration`
- `humidity`

The `faulty` column was not used to train the algorithms.  
It was used only at the end to evaluate how well each algorithm matched the actual faulty rows.

---

## Step 1 — Prepared the Data

We selected the four sensor columns:

- `temperature`
- `pressure`
- `vibration`
- `humidity`

Then we scaled the sensor values using `StandardScaler`.

Scaling was important because some algorithms compare distances or relationships between rows.

After scaling:

- each sensor column had approximately mean `0`
- each sensor column had approximately standard deviation `1`

This made the sensor columns comparable.

---

## Step 2 — Z-Score Outlier Detection

Z-Score is a simple statistical method.

It checks how far each value is from the column average.

A row was marked as an outlier if at least one sensor had:

`absolute Z-Score > 3`

Z-Score detected:

- **467 outlier rows**
- **6.09%** of the dataset

Z-Score worked very well for this dataset because faulty sensor readings were often statistically extreme.

---

## Step 3 — Isolation Forest

Isolation Forest is a tree-based outlier detection algorithm.

It tries to isolate unusual rows using random splits.

Simple idea:

- normal rows are harder to isolate
- unusual rows are easier to isolate

Isolation Forest detected:

- **384 outlier rows**
- **5.01%** of the dataset

This matched the `contamination = 0.05` setting.

---

## Step 4 — LOF: Local Outlier Factor

LOF compares each row with nearby rows.

Simple idea:

- normal rows look similar to their neighbors
- outlier rows look unusual compared to nearby rows

LOF detected:

- **384 outlier rows**
- **5.01%** of the dataset

LOF detected a different type of anomaly compared with Isolation Forest.

---

## Step 5 — ABOD: Angle-Based Outlier Detection

ABOD uses angles and geometric position.

Simple idea:

- normal rows are surrounded by other rows from many directions
- outlier rows sit in unusual geometric positions

ABOD detected:

- **384 outlier rows**
- **5.01%** of the dataset

ABOD helped us detect angle-based unusual sensor patterns.

---

## Step 6 — CBLOF: Cluster-Based Local Outlier Factor

CBLOF uses clustering logic.

Simple idea:

- it groups similar rows into clusters
- rows in strange small clusters can be suspicious
- rows far from cluster centers can also be suspicious

CBLOF detected:

- **384 outlier rows**
- **5.01%** of the dataset

CBLOF helped us detect cluster-based unusual sensor behavior.

---

## Step 7 — LoOP: Local Outlier Probability

LoOP gives each row a probability-style anomaly score.

Simple idea:

- low score = likely normal
- high score = likely unusual

We marked the top 5% highest LoOP scores as outliers.

LoOP detected:

- **384 outlier rows**
- **5.01%** of the dataset

The LoOP threshold used was:

`0.5408`

LoOP detected local-neighborhood anomalies.

---

## Step 8 — PCA Visualizations

We used PCA to compress the four sensor columns into two visual components:

- `PC1`
- `PC2`

Together, PC1 and PC2 explained approximately:

**53.41%** of the sensor variation.

PCA helped us visually inspect where outliers appeared in the sensor space.

Important note:

PCA was used only for visualization.  
It does not show 100% of the original sensor information.

---

## Step 9 — Agreement Between ABOD, CBLOF, and LoOP

ABOD, CBLOF, and LoOP each detected 384 outliers.

However, they did not detect exactly the same rows.

We counted how many algorithms flagged each row.

The results were:

| Category | Rows | Percentage |
|---|---:|---:|
| Normal by ABOD, CBLOF, and LoOP | 6,870 | 89.55% |
| Flagged by 1 algorithm | 471 | 6.14% |
| Flagged by 2 algorithms | 312 | 4.07% |
| Flagged by ABOD, CBLOF, and LoOP | 19 | 0.25% |

The most important group is:

**Flagged by ABOD, CBLOF, and LoOP**

Only **19 rows** were flagged by all three algorithms.

These are high-priority anomaly candidates because three different algorithms agreed that they were unusual.

---

## Step 10 — Pairwise Agreement Between ABOD, CBLOF, and LoOP

We used the Jaccard score to compare how much the algorithms agreed.

Jaccard means:

`shared outliers / total unique outliers`

The results were:

| Algorithm Pair | Shared Outliers | Jaccard Score |
|---|---:|---:|
| ABOD vs CBLOF | 237 | 0.4463 |
| ABOD vs LoOP | 113 | 0.1725 |
| CBLOF vs LoOP | 19 | 0.0254 |

Main interpretation:

- ABOD and CBLOF agreed the most.
- LoOP detected a very different type of anomaly.
- CBLOF and LoOP had very low agreement.

This shows that different algorithms define “unusual” in different ways.

---

## Step 11 — Master Comparison Against the Faulty Label

Finally, we compared all algorithms against the available `faulty` label.

The algorithms were evaluated using:

- Precision
- Recall
- F1-score

Precision means:

“How many flagged rows were actually faulty?”

Recall means:

“How many actual faulty rows were successfully found?”

F1-score means:

“The balance between precision and recall.”

The final results were:

| Algorithm | Precision | Recall | F1-Score |
|---|---:|---:|---:|
| Z-Score | 0.9914 | 0.6037 | 0.7504 |
| CBLOF | 1.0000 | 0.5007 | 0.6672 |
| Isolation Forest | 1.0000 | 0.5007 | 0.6672 |
| ABOD | 0.9453 | 0.4733 | 0.6308 |
| LOF | 0.6432 | 0.3220 | 0.4292 |
| LoOP | 0.4766 | 0.2386 | 0.3180 |

---

## Final Winner — Ultimate Hero

The best-performing algorithm was:

# Z-Score

Z-Score achieved:

- Precision: **0.9914**
- Recall: **0.6037**
- F1-score: **0.7504**

Z-Score had the best overall balance between finding faulty rows and avoiding false alarms.

This means that, for this specific Industrial Equipment dataset, the simple statistical Z-Score method performed better than the advanced outlier detection algorithms.

---

## Final Business Interpretation

The results show that simple methods can sometimes perform better than advanced algorithms.

For this dataset, faulty equipment rows were often connected to extreme sensor readings.  
That is why Z-Score performed strongly.

However, this does not mean Z-Score is always the best method.

Different algorithms detect different types of unusual behavior:

- Z-Score detects extreme individual sensor values.
- Isolation Forest detects rows that are easy to isolate.
- LOF detects locally unusual rows.
- ABOD detects unusual geometric positions.
- CBLOF detects unusual cluster behavior.
- LoOP detects local probability-based anomalies.

In real machine monitoring, outlier detection should be used as an investigation tool.

Rows flagged by multiple algorithms should be inspected first, but rows flagged by only one algorithm should not be ignored because each algorithm captures a different type of abnormal behavior.