# Z-Score Outlier Detection — Process Summary

## Goal of the Z-Score Method

The goal of the Z-Score method is to detect rows where sensor readings are statistically unusual.

A row is one **data point**, meaning one machine observation in the dataset.

For this analysis, we used only the sensor columns:

- `temperature`
- `pressure`
- `vibration`
- `humidity`

---

## Why We Excluded `faulty`

The column `faulty` was excluded from the Z-Score calculation because it is the label/answer column.

It tells us whether the equipment was faulty or not:

- `0` = not faulty
- `1` = faulty

Since `faulty` is not a sensor measurement, it should not be used for statistical outlier detection.

---

## Step 1 — Created a Safe Copy

We created a copy of the original dataframe:

```python
df_zscore = df.copy()
```

This keeps the original dataframe unchanged and allows us to safely add Z-Score columns and outlier flags.

---

## Step 2 — Calculated Z-Scores

For each sensor column, we calculated the Z-Score using the formula:

```text
Z-Score = (value - column mean) / column standard deviation
```

The Z-Score tells us how far each value is from the average of its own column.

Interpretation:

- Z-Score close to `0` = value is close to the average
- Positive Z-Score = value is above the average
- Negative Z-Score = value is below the average
- Absolute Z-Score greater than `3` = statistically unusual value

---

## Step 3 — Added Z-Score Columns

We added one Z-Score column for each sensor:

- `temperature_zscore`
- `pressure_zscore`
- `vibration_zscore`
- `humidity_zscore`

This allowed us to compare each original sensor value with its standardized Z-Score value.

---

## Step 4 — Created the Outlier Flag

We created a new column:

```python
zscore_outlier
```

A row was marked as an outlier if **any sensor column** had:

```text
absolute Z-Score > 3
```

This means a row could be marked as an outlier because of unusually high or low values in temperature, pressure, vibration, or humidity.

---

## Step 5 — Counted Z-Score Outliers

The Z-Score method detected:

- Total rows: **7,672**
- Z-Score outlier rows: **467**
- Outlier percentage: **6.09%**

This means around 6 out of every 100 rows were statistically unusual according to the Z-Score rule.

---

## Step 6 — Checked Which Sensors Caused the Outliers

The number of threshold crossings by sensor was:

| Sensor Z-Score Column | Threshold Crossings |
|---|---:|
| `temperature_zscore` | 235 |
| `vibration_zscore` | 193 |
| `pressure_zscore` | 123 |
| `humidity_zscore` | 96 |

`temperature` and `vibration` contributed the most to the detected Z-Score outliers.

---

## Step 7 — Built Professional Charts

We created several charts to understand the Z-Score outliers visually:

- Sensor contribution chart
- Normal vs outlier chart
- Temperature boxplot with outliers highlighted
- Z-Score distribution chart
- Temperature vs vibration scatter plot
- Z-Score heatmap
- Standard deviation before/after chart

These charts helped us understand both the number of outliers and the sensor patterns behind them.

---

## Step 8 — Removed Z-Score Outliers

We created a cleaned dataframe:

```python
df_zscore_clean
```

This dataframe contains only rows where:

```python
zscore_outlier == False
```

After removing outliers:

- Rows before removal: **7,672**
- Rows after removal: **7,205**
- Rows removed: **467**
- Percentage removed: **6.09%**

---

## Step 9 — Compared Before vs After Removing Outliers

After removing Z-Score outliers, the standard deviation decreased for every sensor.

| Sensor | Standard Deviation Reduction |
|---|---:|
| Temperature | **-29.42%** |
| Vibration | **-24.84%** |
| Pressure | **-16.82%** |
| Humidity | **-11.77%** |

This shows that the outliers were increasing the spread of the sensor values, especially for `temperature` and `vibration`.

---

## Final Interpretation

The Z-Score method helped us identify statistically unusual sensor readings.

Removing these rows made the dataset less spread out and more statistically stable.

However, in industrial equipment monitoring, outliers should **not** be deleted blindly. Some unusual rows may represent real machine problems, early fault signals, sensor errors, or rare operating conditions.

Therefore, Z-Score outlier detection should be treated as an investigation step, not an automatic deletion rule.
