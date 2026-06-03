# Quick Reference Map — Master Outlier Comparison

```text
Original CSV file
equipment_anomaly_data.csv
        |
        v
df
Original full dataset
temperature, pressure, vibration, humidity, equipment, location, faulty
        |
        v
sensor_columns
["temperature", "pressure", "vibration", "humidity"]
        |
        v
X
Only sensor columns
Used for Z-Score
        |
        v
X_scaled
Scaled sensor values
Used for model-based algorithms


Algorithm Result Map

X
|
|--> Z-Score
|       |
|       v
|   zscore_outlier
|
X_scaled
|
|--> Isolation Forest
|       |
|       v
|   isolation_forest_outlier
|
|--> LOF
|       |
|       v
|   lof_outlier
|
|--> ABOD
|       |
|       v
|   abod_outlier
|
|--> CBLOF
|       |
|       v
|   cblof_outlier
|
|--> LoOP
        |
        v
    loop_outlier


Master DataFrame Map

df_extended

Already contains:
abod_outlier
cblof_outlier
loop_outlier
faulty
        |
        v
df_master = df_extended.copy()
        |
        v
Add recreated results:

zscore_outlier
isolation_forest_outlier
lof_outlier
        |
        v
df_master now contains all algorithm results

df_master
        |
        v
Compare each outlier column with faulty
        |
        v
precision
recall
f1_score
        |
        v
master_comparison_sorted
        |
        v
Master comparison chart
        |
        v
Ultimate Hero = Z-Score