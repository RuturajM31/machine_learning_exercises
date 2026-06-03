<div style="
background:#111827;
color:#e5e7eb;
border-radius:16px;
font-family:Arial, sans-serif;
line-height:1.6;
border:1px solid #374151;
overflow:hidden;
">

<!-- Header -->
<div style="
background:#0b1220;
padding:22px 28px;
border-bottom:1px solid #374151;
">
<div style="
font-size:12px;
letter-spacing:1.3px;
text-transform:uppercase;
color:#9ca3af;
font-weight:700;
margin-bottom:8px;
">
Expert Section Summary
</div>

<h1 style="
color:#f9fafb;
margin:0;
font-size:26px;
font-weight:800;
line-height:1.25;
">
KDD Cup 1999 Autoencoder Anomaly Detection — Complete Workflow
</h1>

<p style="
color:#9ca3af;
margin:10px 0 0 0;
font-size:14px;
">
Prepared by <strong style="color:#d1d5db;">Ruturaj Mokashi</strong>
</p>
</div>

<!-- Body -->
<div style="padding:28px;">

<h2 style="color:#f3f4f6; font-size:18px; border-left:4px solid #6b7280; padding-left:12px;">
Project Goal
</h2>

<p>
The goal of this project was to detect suspicious network connections using an <strong>Autoencoder</strong>.
</p>

<p>
The KDD Cup 1999 dataset contains network connection records. Each row represents one network connection. The target label tells whether the connection is normal or attack-like.
</p>

<pre style="
background:#0f172a;
color:#e5e7eb;
padding:16px;
border-radius:10px;
border:1px solid #374151;
overflow:auto;
">
Train Autoencoder on normal network traffic
        ↓
Learn normal connection behavior
        ↓
Reconstruct test connections
        ↓
Calculate reconstruction error
        ↓
High reconstruction error = possible anomaly
</pre>

<hr style="border:0; border-top:1px solid #374151; margin:26px 0;">

<h2 style="color:#f3f4f6; font-size:18px; border-left:4px solid #6b7280; padding-left:12px;">
Step 1 — Load Dataset
</h2>

<pre style="
background:#0f172a;
color:#e5e7eb;
padding:16px;
border-radius:10px;
border:1px solid #374151;
overflow:auto;
">
kdd_data = fetch_kddcup99(
    percent10=True,
    as_frame=True,
    shuffle=True,
    random_state=RANDOM_STATE
)

X_kdd_raw = kdd_data.data.copy()
y_kdd_raw = kdd_data.target.copy()
</pre>

<table style="width:100%; border-collapse:collapse; color:#f9fafb; margin:18px 0; font-size:14px;">
<tr style="background:#1f2937;">
<th style="text-align:left; padding:10px; border:1px solid #4b5563; color:#f9fafb;">Variable</th>
<th style="text-align:left; padding:10px; border:1px solid #4b5563; color:#f9fafb;">Meaning</th>
</tr>
<tr>
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;"><code>X_kdd_raw</code></td>
<td style="padding:10px; border:1px solid #4b5563; color:#e5e7eb;">Raw feature data with 41 columns.</td>
</tr>
<tr style="background:#0f172a;">
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;"><code>y_kdd_raw</code></td>
<td style="padding:10px; border:1px solid #4b5563; color:#e5e7eb;">Original target labels such as normal, smurf, neptune, etc.</td>
</tr>
</table>

<p>
The dataset contained <strong style="color:#ffffff;">494,021 rows</strong> and <strong style="color:#ffffff;">41 original feature columns</strong>.
</p>

<hr style="border:0; border-top:1px solid #374151; margin:26px 0;">

<h2 style="color:#f3f4f6; font-size:18px; border-left:4px solid #6b7280; padding-left:12px;">
Step 2 — Convert Labels into Normal vs Anomaly
</h2>

<p>
The original labels had many attack names. We simplified them into a binary target.
</p>

<pre style="
background:#0f172a;
color:#e5e7eb;
padding:16px;
border-radius:10px;
border:1px solid #374151;
overflow:auto;
">
y_kdd = y_kdd_raw.astype(str)

y_kdd_clean = cleaned version of y_kdd

y_kdd_binary = np.where(y_kdd_clean == "normal", 0, 1)
</pre>

<table style="width:100%; border-collapse:collapse; color:#f9fafb; margin:18px 0; font-size:14px;">
<tr style="background:#1f2937;">
<th style="text-align:left; padding:10px; border:1px solid #4b5563; color:#f9fafb;">Class</th>
<th style="text-align:left; padding:10px; border:1px solid #4b5563; color:#f9fafb;">Rows</th>
<th style="text-align:left; padding:10px; border:1px solid #4b5563; color:#f9fafb;">Percentage</th>
</tr>
<tr>
<td style="padding:10px; border:1px solid #4b5563; color:#e5e7eb;">Normal</td>
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;">97,278</td>
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;">19.69%</td>
</tr>
<tr style="background:#0f172a;">
<td style="padding:10px; border:1px solid #4b5563; color:#e5e7eb;">Anomaly</td>
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;">396,743</td>
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;">80.31%</td>
</tr>
</table>

<p>
Binary target meaning:
</p>

<ul>
<li><code>0</code> = Normal network connection</li>
<li><code>1</code> = Anomaly / attack connection</li>
</ul>

<hr style="border:0; border-top:1px solid #374151; margin:26px 0;">

<h2 style="color:#f3f4f6; font-size:18px; border-left:4px solid #6b7280; padding-left:12px;">
Step 3 — Correct Feature Types
</h2>

<p>
At first, all 41 columns appeared as categorical because many numeric values were loaded as text.
</p>

<p>
We corrected the feature types manually.
</p>

<pre style="
background:#0f172a;
color:#e5e7eb;
padding:16px;
border-radius:10px;
border:1px solid #374151;
overflow:auto;
">
categorical_columns = ["protocol_type", "service", "flag"]

numerical_columns = [
    col for col in X_kdd_clean.columns
    if col not in categorical_columns
]

X_kdd_clean = X_kdd_raw.copy()

for col in numerical_columns:
    X_kdd_clean[col] = pd.to_numeric(X_kdd_clean[col], errors="coerce")
</pre>

<table style="width:100%; border-collapse:collapse; color:#f9fafb; margin:18px 0; font-size:14px;">
<tr style="background:#1f2937;">
<th style="text-align:left; padding:10px; border:1px solid #4b5563; color:#f9fafb;">Variable</th>
<th style="text-align:left; padding:10px; border:1px solid #4b5563; color:#f9fafb;">Meaning</th>
</tr>
<tr>
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;"><code>X_kdd_clean</code></td>
<td style="padding:10px; border:1px solid #4b5563; color:#e5e7eb;">Cleaned feature dataframe with corrected types.</td>
</tr>
<tr style="background:#0f172a;">
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;"><code>corrected_numerical_columns</code></td>
<td style="padding:10px; border:1px solid #4b5563; color:#e5e7eb;">38 numerical columns used for scaling.</td>
</tr>
<tr>
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;"><code>corrected_categorical_columns</code></td>
<td style="padding:10px; border:1px solid #4b5563; color:#e5e7eb;">3 categorical columns used for one-hot encoding.</td>
</tr>
</table>

<p>
Final feature structure:
</p>

<ul>
<li><strong style="color:#ffffff;">38 numerical columns</strong></li>
<li><strong style="color:#ffffff;">3 categorical columns</strong>: <code>protocol_type</code>, <code>service</code>, <code>flag</code></li>
</ul>

<hr style="border:0; border-top:1px solid #374151; margin:26px 0;">

<h2 style="color:#f3f4f6; font-size:18px; border-left:4px solid #6b7280; padding-left:12px;">
Step 4 — Train/Test Split
</h2>

<pre style="
background:#0f172a;
color:#e5e7eb;
padding:16px;
border-radius:10px;
border:1px solid #374151;
overflow:auto;
">
X_train_raw, X_test_raw, y_train, y_test = train_test_split(
    X_kdd_clean,
    y_kdd_binary,
    test_size=0.20,
    random_state=RANDOM_STATE,
    stratify=y_kdd_binary
)

X_train_normal_raw = X_train_raw[y_train == 0].copy()
</pre>

<table style="width:100%; border-collapse:collapse; color:#f9fafb; margin:18px 0; font-size:14px;">
<tr style="background:#1f2937;">
<th style="text-align:left; padding:10px; border:1px solid #4b5563; color:#f9fafb;">Variable</th>
<th style="text-align:left; padding:10px; border:1px solid #4b5563; color:#f9fafb;">Rows</th>
<th style="text-align:left; padding:10px; border:1px solid #4b5563; color:#f9fafb;">Purpose</th>
</tr>
<tr>
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;"><code>X_train_raw</code></td>
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;">395,216</td>
<td style="padding:10px; border:1px solid #4b5563; color:#e5e7eb;">Full training features.</td>
</tr>
<tr style="background:#0f172a;">
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;"><code>X_test_raw</code></td>
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;">98,805</td>
<td style="padding:10px; border:1px solid #4b5563; color:#e5e7eb;">Test features.</td>
</tr>
<tr>
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;"><code>X_train_normal_raw</code></td>
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;">77,822</td>
<td style="padding:10px; border:1px solid #4b5563; color:#e5e7eb;">Only normal rows used to train the Autoencoder.</td>
</tr>
</table>

<p>
The Autoencoder was trained on normal rows only because it should learn normal network behavior.
</p>

<hr style="border:0; border-top:1px solid #374151; margin:26px 0;">

<h2 style="color:#f3f4f6; font-size:18px; border-left:4px solid #6b7280; padding-left:12px;">
Step 5 — Preprocess Features
</h2>

<p>
The Autoencoder needs fully numeric input. We scaled numerical columns and one-hot encoded categorical columns.
</p>

<pre style="
background:#0f172a;
color:#e5e7eb;
padding:16px;
border-radius:10px;
border:1px solid #374151;
overflow:auto;
">
numeric_pipeline = Pipeline([
    ("imputer", SimpleImputer(strategy="median")),
    ("scaler", StandardScaler())
])

categorical_pipeline = Pipeline([
    ("imputer", SimpleImputer(strategy="most_frequent")),
    ("onehot", OneHotEncoder(handle_unknown="ignore"))
])

preprocessor = ColumnTransformer([
    ("numeric", numeric_pipeline, corrected_numerical_columns),
    ("categorical", categorical_pipeline, corrected_categorical_columns)
])

preprocessor.fit(X_train_normal_raw)
</pre>

<p>
Then we transformed the datasets:
</p>

<pre style="
background:#0f172a;
color:#e5e7eb;
padding:16px;
border-radius:10px;
border:1px solid #374151;
overflow:auto;
">
X_train_normal_processed = preprocessor.transform(X_train_normal_raw)
X_train_processed        = preprocessor.transform(X_train_raw)
X_test_processed         = preprocessor.transform(X_test_raw)
</pre>

<table style="width:100%; border-collapse:collapse; color:#f9fafb; margin:18px 0; font-size:14px;">
<tr style="background:#1f2937;">
<th style="text-align:left; padding:10px; border:1px solid #4b5563; color:#f9fafb;">Processed Variable</th>
<th style="text-align:left; padding:10px; border:1px solid #4b5563; color:#f9fafb;">Shape</th>
<th style="text-align:left; padding:10px; border:1px solid #4b5563; color:#f9fafb;">Use</th>
</tr>
<tr>
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;"><code>X_train_normal_processed</code></td>
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;">77,822 × 74</td>
<td style="padding:10px; border:1px solid #4b5563; color:#e5e7eb;">Used to train the Autoencoder.</td>
</tr>
<tr style="background:#0f172a;">
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;"><code>X_train_processed</code></td>
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;">395,216 × 74</td>
<td style="padding:10px; border:1px solid #4b5563; color:#e5e7eb;">Full processed training data.</td>
</tr>
<tr>
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;"><code>X_test_processed</code></td>
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;">98,805 × 74</td>
<td style="padding:10px; border:1px solid #4b5563; color:#e5e7eb;">Used for final testing and predictions.</td>
</tr>
</table>

<p>
The original 41 columns became <strong style="color:#ffffff;">74 processed features</strong> after one-hot encoding.
</p>

<hr style="border:0; border-top:1px solid #374151; margin:26px 0;">

<h2 style="color:#f3f4f6; font-size:18px; border-left:4px solid #6b7280; padding-left:12px;">
Step 6 — Build Autoencoder
</h2>

<pre style="
background:#0f172a;
color:#e5e7eb;
padding:16px;
border-radius:10px;
border:1px solid #374151;
overflow:auto;
">
input_dim = X_train_normal_processed.shape[1]

autoencoder = keras.Sequential([
    layers.Input(shape=(input_dim,)),
    layers.Dense(64, activation="relu"),
    layers.Dense(32, activation="relu"),
    layers.Dense(16, activation="relu"),
    layers.Dense(32, activation="relu"),
    layers.Dense(64, activation="relu"),
    layers.Dense(input_dim, activation="linear")
])

autoencoder.compile(
    optimizer="adam",
    loss="mse"
)
</pre>

<pre style="
background:#0f172a;
color:#e5e7eb;
padding:16px;
border-radius:10px;
border:1px solid #374151;
overflow:auto;
">
Input: 74 features
        ↓
Encoder: 64 → 32
        ↓
Bottleneck: 16
        ↓
Decoder: 32 → 64
        ↓
Output: 74 reconstructed features
</pre>

<p>
The model had <strong style="color:#ffffff;">14,874 trainable parameters</strong>.
</p>

<hr style="border:0; border-top:1px solid #374151; margin:26px 0;">

<h2 style="color:#f3f4f6; font-size:18px; border-left:4px solid #6b7280; padding-left:12px;">
Step 7 — Train Autoencoder
</h2>

<p>
The Autoencoder was trained to reconstruct normal data.
</p>

<pre style="
background:#0f172a;
color:#e5e7eb;
padding:16px;
border-radius:10px;
border:1px solid #374151;
overflow:auto;
">
history = autoencoder.fit(
    X_train_normal_processed,
    X_train_normal_processed,
    epochs=20,
    batch_size=256,
    validation_split=0.20,
    shuffle=True
)
</pre>

<table style="width:100%; border-collapse:collapse; color:#f9fafb; margin:18px 0; font-size:14px;">
<tr style="background:#1f2937;">
<th style="text-align:left; padding:10px; border:1px solid #4b5563; color:#f9fafb;">Training Result</th>
<th style="text-align:left; padding:10px; border:1px solid #4b5563; color:#f9fafb;">Value</th>
</tr>
<tr>
<td style="padding:10px; border:1px solid #4b5563; color:#e5e7eb;">Final training loss</td>
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;">0.026720</td>
</tr>
<tr style="background:#0f172a;">
<td style="padding:10px; border:1px solid #4b5563; color:#e5e7eb;">Final validation loss</td>
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;">0.171016</td>
</tr>
</table>

<hr style="border:0; border-top:1px solid #374151; margin:26px 0;">

<h2 style="color:#f3f4f6; font-size:18px; border-left:4px solid #6b7280; padding-left:12px;">
Step 8 — Calculate Reconstruction Error
</h2>

<pre style="
background:#0f172a;
color:#e5e7eb;
padding:16px;
border-radius:10px;
border:1px solid #374151;
overflow:auto;
">
X_test_reconstructed = autoencoder.predict(X_test_processed)

test_reconstruction_error = np.mean(
    np.square(X_test_processed - X_test_reconstructed),
    axis=1
)
</pre>

<pre style="
background:#0f172a;
color:#e5e7eb;
padding:16px;
border-radius:10px;
border:1px solid #374151;
overflow:auto;
">
reconstruction_results = pd.DataFrame({
    "true_label": y_test,
    "connection_type": Normal or Anomaly,
    "reconstruction_error": test_reconstruction_error
})
</pre>

<table style="width:100%; border-collapse:collapse; color:#f9fafb; margin:18px 0; font-size:14px;">
<tr style="background:#1f2937;">
<th style="text-align:left; padding:10px; border:1px solid #4b5563; color:#f9fafb;">Connection Type</th>
<th style="text-align:left; padding:10px; border:1px solid #4b5563; color:#f9fafb;">Median Error</th>
<th style="text-align:left; padding:10px; border:1px solid #4b5563; color:#f9fafb;">Meaning</th>
</tr>
<tr>
<td style="padding:10px; border:1px solid #4b5563; color:#e5e7eb;">Normal</td>
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;">0.003227</td>
<td style="padding:10px; border:1px solid #4b5563; color:#e5e7eb;">Autoencoder reconstructs normal rows well.</td>
</tr>
<tr style="background:#0f172a;">
<td style="padding:10px; border:1px solid #4b5563; color:#e5e7eb;">Anomaly</td>
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;">0.307520</td>
<td style="padding:10px; border:1px solid #4b5563; color:#e5e7eb;">Autoencoder reconstructs anomaly rows worse.</td>
</tr>
</table>

<p>
Reconstruction error became the anomaly score.
</p>

<hr style="border:0; border-top:1px solid #374151; margin:26px 0;">

<h2 style="color:#f3f4f6; font-size:18px; border-left:4px solid #6b7280; padding-left:12px;">
Step 9 — Choose Threshold and Predict Anomalies
</h2>

<pre style="
background:#0f172a;
color:#e5e7eb;
padding:16px;
border-radius:10px;
border:1px solid #374151;
overflow:auto;
">
X_train_normal_reconstructed = autoencoder.predict(X_train_normal_processed)

train_normal_reconstruction_error = np.mean(
    np.square(X_train_normal_processed - X_train_normal_reconstructed),
    axis=1
)

anomaly_threshold = np.percentile(train_normal_reconstruction_error, 95)

reconstruction_results["predicted_label"] = (
    reconstruction_results["reconstruction_error"] > anomaly_threshold
).astype(int)
</pre>

<table style="width:100%; border-collapse:collapse; color:#f9fafb; margin:18px 0; font-size:14px;">
<tr style="background:#1f2937;">
<th style="text-align:left; padding:10px; border:1px solid #4b5563; color:#f9fafb;">Prediction</th>
<th style="text-align:left; padding:10px; border:1px solid #4b5563; color:#f9fafb;">Rows</th>
<th style="text-align:left; padding:10px; border:1px solid #4b5563; color:#f9fafb;">Percentage</th>
</tr>
<tr>
<td style="padding:10px; border:1px solid #4b5563; color:#e5e7eb;">Predicted Anomaly</td>
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;">80,198</td>
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;">81.17%</td>
</tr>
<tr style="background:#0f172a;">
<td style="padding:10px; border:1px solid #4b5563; color:#e5e7eb;">Predicted Normal</td>
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;">18,607</td>
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;">18.83%</td>
</tr>
</table>

<hr style="border:0; border-top:1px solid #374151; margin:26px 0;">

<h2 style="color:#f3f4f6; font-size:18px; border-left:4px solid #6b7280; padding-left:12px;">
Step 10 — Evaluate Autoencoder
</h2>

<pre style="
background:#0f172a;
color:#e5e7eb;
padding:16px;
border-radius:10px;
border:1px solid #374151;
overflow:auto;
">
y_true_autoencoder = reconstruction_results["true_label"].astype(int)
y_pred_autoencoder = reconstruction_results["predicted_label"].astype(int)

precision_score()
recall_score()
f1_score()
accuracy_score()
confusion_matrix()
</pre>

<table style="width:100%; border-collapse:collapse; color:#f9fafb; margin:18px 0; font-size:14px;">
<tr style="background:#1f2937;">
<th style="text-align:left; padding:10px; border:1px solid #4b5563; color:#f9fafb;">Metric</th>
<th style="text-align:left; padding:10px; border:1px solid #4b5563; color:#f9fafb;">Autoencoder Result</th>
</tr>
<tr>
<td style="padding:10px; border:1px solid #4b5563; color:#e5e7eb;">Precision</td>
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;">0.9879</td>
</tr>
<tr style="background:#0f172a;">
<td style="padding:10px; border:1px solid #4b5563; color:#e5e7eb;">Recall</td>
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;">0.9984</td>
</tr>
<tr>
<td style="padding:10px; border:1px solid #4b5563; color:#e5e7eb;">F1-score</td>
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;">0.9931</td>
</tr>
<tr style="background:#0f172a;">
<td style="padding:10px; border:1px solid #4b5563; color:#e5e7eb;">Accuracy</td>
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;">0.9889</td>
</tr>
</table>

<table style="width:100%; border-collapse:collapse; color:#f9fafb; margin:18px 0; font-size:14px;">
<tr style="background:#1f2937;">
<th style="text-align:left; padding:10px; border:1px solid #4b5563; color:#f9fafb;">Outcome</th>
<th style="text-align:left; padding:10px; border:1px solid #4b5563; color:#f9fafb;">Rows</th>
</tr>
<tr>
<td style="padding:10px; border:1px solid #4b5563; color:#e5e7eb;">Correct Normal</td>
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;">18,482</td>
</tr>
<tr style="background:#0f172a;">
<td style="padding:10px; border:1px solid #4b5563; color:#e5e7eb;">False Alarm</td>
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;">974</td>
</tr>
<tr>
<td style="padding:10px; border:1px solid #4b5563; color:#e5e7eb;">Missed Attack</td>
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;">125</td>
</tr>
<tr style="background:#0f172a;">
<td style="padding:10px; border:1px solid #4b5563; color:#e5e7eb;">Correct Attack</td>
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;">79,224</td>
</tr>
</table>

<hr style="border:0; border-top:1px solid #374151; margin:26px 0;">

<h2 style="color:#f3f4f6; font-size:18px; border-left:4px solid #6b7280; padding-left:12px;">
Step 11 — Build Isolation Forest Baseline
</h2>

<p>
To compare the Autoencoder with a traditional anomaly detection algorithm, we trained Isolation Forest on normal training rows.
</p>

<pre style="
background:#0f172a;
color:#e5e7eb;
padding:16px;
border-radius:10px;
border:1px solid #374151;
overflow:auto;
">
isolation_forest_kdd = IsolationForest(
    n_estimators=100,
    contamination="auto",
    random_state=RANDOM_STATE,
    n_jobs=-1
)

isolation_forest_kdd.fit(X_train_normal_processed)

train_normal_if_scores = -isolation_forest_kdd.score_samples(X_train_normal_processed)

if_threshold = np.percentile(train_normal_if_scores, 95)

test_if_scores = -isolation_forest_kdd.score_samples(X_test_processed)

reconstruction_results["if_predicted_label"] = (
    reconstruction_results["if_anomaly_score"] > if_threshold
).astype(int)
</pre>

<hr style="border:0; border-top:1px solid #374151; margin:26px 0;">

<h2 style="color:#f3f4f6; font-size:18px; border-left:4px solid #6b7280; padding-left:12px;">
Step 12 — Final Model Comparison
</h2>

<table style="width:100%; border-collapse:collapse; color:#f9fafb; margin:18px 0; font-size:14px;">
<tr style="background:#1f2937;">
<th style="text-align:left; padding:10px; border:1px solid #4b5563; color:#f9fafb;">Model</th>
<th style="text-align:left; padding:10px; border:1px solid #4b5563; color:#f9fafb;">Precision</th>
<th style="text-align:left; padding:10px; border:1px solid #4b5563; color:#f9fafb;">Recall</th>
<th style="text-align:left; padding:10px; border:1px solid #4b5563; color:#f9fafb;">F1-score</th>
<th style="text-align:left; padding:10px; border:1px solid #4b5563; color:#f9fafb;">Accuracy</th>
</tr>
<tr>
<td style="padding:10px; border:1px solid #4b5563; color:#e5e7eb;">Autoencoder</td>
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;">0.9879</td>
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;">0.9984</td>
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;">0.9931</td>
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;">0.9889</td>
</tr>
<tr style="background:#0f172a;">
<td style="padding:10px; border:1px solid #4b5563; color:#e5e7eb;">Isolation Forest</td>
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;">0.9886</td>
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;">0.9903</td>
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;">0.9894</td>
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;">0.9830</td>
</tr>
</table>

<table style="width:100%; border-collapse:collapse; color:#f9fafb; margin:18px 0; font-size:14px;">
<tr style="background:#1f2937;">
<th style="text-align:left; padding:10px; border:1px solid #4b5563; color:#f9fafb;">Model</th>
<th style="text-align:left; padding:10px; border:1px solid #4b5563; color:#f9fafb;">False Alarms</th>
<th style="text-align:left; padding:10px; border:1px solid #4b5563; color:#f9fafb;">Missed Attacks</th>
</tr>
<tr>
<td style="padding:10px; border:1px solid #4b5563; color:#e5e7eb;">Autoencoder</td>
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;">974</td>
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;">125</td>
</tr>
<tr style="background:#0f172a;">
<td style="padding:10px; border:1px solid #4b5563; color:#e5e7eb;">Isolation Forest</td>
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;">910</td>
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;">773</td>
</tr>
</table>

<div style="
background:#1f2937;
border:1px solid #4b5563;
border-left:4px solid #9ca3af;
padding:18px;
border-radius:12px;
margin-top:24px;
">

<h2 style="
color:#f9fafb;
font-size:18px;
margin-top:0;
">
Final Result — Autoencoder Wins
</h2>

<p>
The Autoencoder performed better overall because it achieved the highest recall and F1-score.
</p>

<p>
In network security, missed attacks are more dangerous than false alarms.
</p>

<p style="margin-bottom:0;">
The Autoencoder missed only <strong style="color:#ffffff;">125 attacks</strong>, while Isolation Forest missed <strong style="color:#ffffff;">773 attacks</strong>. Therefore, the Autoencoder is the stronger model for this KDD Cup 1999 anomaly detection task.
</p>

</div>

</div>
</div>