Goal of Z-Score method

Detect rows where sensor readings are statistically unusual.
A row is one data point.

We used the sensor columns only: temperature, pressure, vibration, humidity.
Why we excluded faulty

faulty is the label/answer column.
It tells whether equipment is faulty or not.
It is not a sensor measurement, so we did not use it for Z-Score calculation.
Step 1: Created a copy
We created df_zscore = df.copy().
This kept the original dataframe safe.

Step 2: Calculated Z-Scores

For each sensor column, we calculated:
Z-Score = (value - column mean) / column standard deviation
This tells how far each value is from the average.
Step 3: Added Z-Score columns
We added:
temperature_zscore
pressure_zscore
vibration_zscore
humidity_zscore

Step 4: Created outlier flag

We created zscore_outlier.
A row was marked True if any sensor had:
absolute Z-Score > 3

Step 5: Counted outliers

Total rows: 7,672
Z-Score outlier rows: 467
Outlier percentage: 6.09%

Step 6: Checked which sensors caused outliers
temperature_zscore: 235
vibration_zscore: 193
pressure_zscore: 123
humidity_zscore: 96
Temperature and vibration contributed the most.

Step 7: Built charts
Sensor contribution chart
Normal vs outlier chart
Temperature boxplot with outliers
Z-Score distribution chart
Temperature vs vibration scatter plot
Z-Score heatmap
Standard deviation before/after chart
Step 8: Removed outliers
Created df_zscore_clean.
Removed rows where zscore_outlier == True.
Rows before: 7,672
Rows after: 7,205
Rows removed: 467

Step 9: Compared before vs after

Standard deviation decreased for every sensor.
Biggest reductions:
Temperature: -29.42%
Vibration: -24.84%
Pressure: -16.82%
Humidity: -11.77%

Final meaning
Z-Score helped us find statistically unusual sensor readings.
Removing them made the dataset less spread out.
But in real machine monitoring, we should not delete outliers blindly, because they may represent real equipment problems.