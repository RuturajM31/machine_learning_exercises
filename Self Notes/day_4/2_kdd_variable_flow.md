<div style="
background:#111827;
color:#e5e7eb;
border-radius:16px;
font-family:Arial, sans-serif;
line-height:1.65;
border:1px solid #374151;
overflow:hidden;
">

<div style="
background:#0b1220;
padding:24px 30px;
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
KDD Cup 1999 — Variable Flow Map
</div>

<h1 style="
color:#f9fafb;
margin:0;
font-size:26px;
font-weight:800;
line-height:1.25;
">
From Raw Data to Autoencoder Predictions
</h1>

<p style="
color:#9ca3af;
margin:10px 0 0 0;
font-size:14px;
">
Prepared by <strong style="color:#d1d5db;">Ruturaj Mokashi</strong>
</p>
</div>

<div style="padding:30px;">

<h2 style="color:#f3f4f6; font-size:19px; border-left:4px solid #6b7280; padding-left:12px;">
Step 1 — Load Raw Data
</h2>

<pre style="
background:#0f172a;
color:#e5e7eb;
padding:16px;
border-radius:10px;
border:1px solid #374151;
overflow:auto;
">
kdd_data = fetch_kddcup99(...)

X_kdd_raw = kdd_data.data.copy()
y_kdd_raw = kdd_data.target.copy()
</pre>

<table style="width:100%; border-collapse:collapse; color:#f9fafb; margin:18px 0; font-size:14px;">
<tr style="background:#1f2937;">
<th style="text-align:left; padding:10px; border:1px solid #4b5563; color:#ffffff;">Variable</th>
<th style="text-align:left; padding:10px; border:1px solid #4b5563; color:#ffffff;">Meaning</th>
</tr>
<tr>
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;"><code>X_kdd_raw</code></td>
<td style="padding:10px; border:1px solid #4b5563; color:#e5e7eb;">Raw network connection features.</td>
</tr>
<tr style="background:#0f172a;">
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;"><code>y_kdd_raw</code></td>
<td style="padding:10px; border:1px solid #4b5563; color:#e5e7eb;">Original labels such as normal, smurf, neptune, etc.</td>
</tr>
</table>

<h2 style="color:#f3f4f6; font-size:19px; border-left:4px solid #6b7280; padding-left:12px;">
Step 2 — Create Binary Target
</h2>

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

<p>
The target was converted into:
</p>

<ul>
<li><code>0</code> = Normal connection</li>
<li><code>1</code> = Anomaly / attack connection</li>
</ul>

<h2 style="color:#f3f4f6; font-size:19px; border-left:4px solid #6b7280; padding-left:12px;">
Step 3 — Clean Feature Types
</h2>

<pre style="
background:#0f172a;
color:#e5e7eb;
padding:16px;
border-radius:10px;
border:1px solid #374151;
overflow:auto;
">
X_kdd_clean = X_kdd_raw.copy()

categorical_columns = ["protocol_type", "service", "flag"]

numerical_columns = all columns except categorical_columns

for col in numerical_columns:
    X_kdd_clean[col] = pd.to_numeric(X_kdd_clean[col], errors="coerce")
</pre>

<table style="width:100%; border-collapse:collapse; color:#f9fafb; margin:18px 0; font-size:14px;">
<tr style="background:#1f2937;">
<th style="text-align:left; padding:10px; border:1px solid #4b5563; color:#ffffff;">Variable</th>
<th style="text-align:left; padding:10px; border:1px solid #4b5563; color:#ffffff;">Meaning</th>
</tr>
<tr>
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;"><code>X_kdd_clean</code></td>
<td style="padding:10px; border:1px solid #4b5563; color:#e5e7eb;">Cleaned feature dataframe with corrected data types.</td>
</tr>
<tr style="background:#0f172a;">
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;"><code>corrected_numerical_columns</code></td>
<td style="padding:10px; border:1px solid #4b5563; color:#e5e7eb;">38 numeric columns used for scaling.</td>
</tr>
<tr>
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;"><code>corrected_categorical_columns</code></td>
<td style="padding:10px; border:1px solid #4b5563; color:#e5e7eb;">3 categorical columns used for one-hot encoding.</td>
</tr>
</table>

<h2 style="color:#f3f4f6; font-size:19px; border-left:4px solid #6b7280; padding-left:12px;">
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
<th style="text-align:left; padding:10px; border:1px solid #4b5563; color:#ffffff;">Variable</th>
<th style="text-align:left; padding:10px; border:1px solid #4b5563; color:#ffffff;">Purpose</th>
</tr>
<tr>
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;"><code>X_train_raw</code></td>
<td style="padding:10px; border:1px solid #4b5563; color:#e5e7eb;">Full raw training features.</td>
</tr>
<tr style="background:#0f172a;">
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;"><code>X_test_raw</code></td>
<td style="padding:10px; border:1px solid #4b5563; color:#e5e7eb;">Raw test features used later for evaluation.</td>
</tr>
<tr>
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;"><code>X_train_normal_raw</code></td>
<td style="padding:10px; border:1px solid #4b5563; color:#e5e7eb;">Only normal training rows. This is used to train the Autoencoder.</td>
</tr>
<tr style="background:#0f172a;">
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;"><code>y_test</code></td>
<td style="padding:10px; border:1px solid #4b5563; color:#e5e7eb;">True test labels used to evaluate predictions.</td>
</tr>
</table>

<h2 style="color:#f3f4f6; font-size:19px; border-left:4px solid #6b7280; padding-left:12px;">
Step 5 — Preprocessing Pipeline
</h2>

<pre style="
background:#0f172a;
color:#e5e7eb;
padding:16px;
border-radius:10px;
border:1px solid #374151;
overflow:auto;
">
numeric_pipeline:
    SimpleImputer(strategy="median")
    StandardScaler()

categorical_pipeline:
    SimpleImputer(strategy="most_frequent")
    OneHotEncoder(handle_unknown="ignore")

preprocessor = ColumnTransformer(...)
preprocessor.fit(X_train_normal_raw)
</pre>

<p>
The preprocessing was fitted on normal training rows only, because the Autoencoder should learn the structure of normal traffic.
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
<th style="text-align:left; padding:10px; border:1px solid #4b5563; color:#ffffff;">Processed Variable</th>
<th style="text-align:left; padding:10px; border:1px solid #4b5563; color:#ffffff;">Shape</th>
<th style="text-align:left; padding:10px; border:1px solid #4b5563; color:#ffffff;">Use</th>
</tr>
<tr>
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;"><code>X_train_normal_processed</code></td>
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;">77,822 × 74</td>
<td style="padding:10px; border:1px solid #4b5563; color:#e5e7eb;">Autoencoder training input.</td>
</tr>
<tr style="background:#0f172a;">
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;"><code>X_test_processed</code></td>
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;">98,805 × 74</td>
<td style="padding:10px; border:1px solid #4b5563; color:#e5e7eb;">Autoencoder and Isolation Forest test input.</td>
</tr>
</table>

<h2 style="color:#f3f4f6; font-size:19px; border-left:4px solid #6b7280; padding-left:12px;">
Step 6 — Autoencoder Flow
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

Autoencoder architecture:

74 input features
        ↓
64 neurons
        ↓
32 neurons
        ↓
16 bottleneck neurons
        ↓
32 neurons
        ↓
64 neurons
        ↓
74 reconstructed features
</pre>

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
    validation_split=0.20
)
</pre>

<p>
Input and target were the same because the Autoencoder learns to reconstruct its input.
</p>

<h2 style="color:#f3f4f6; font-size:19px; border-left:4px solid #6b7280; padding-left:12px;">
Step 7 — Reconstruction Error and Prediction
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

test_reconstruction_error = mean squared difference between:
    X_test_processed
    X_test_reconstructed
</pre>

<pre style="
background:#0f172a;
color:#e5e7eb;
padding:16px;
border-radius:10px;
border:1px solid #374151;
overflow:auto;
">
reconstruction_results = dataframe containing:

true_label
connection_type
reconstruction_error
predicted_label
</pre>

<p>
Threshold logic:
</p>

<pre style="
background:#0f172a;
color:#e5e7eb;
padding:16px;
border-radius:10px;
border:1px solid #374151;
overflow:auto;
">
anomaly_threshold = 95th percentile of normal training reconstruction error

if reconstruction_error > anomaly_threshold:
    predicted_label = 1
else:
    predicted_label = 0
</pre>

<div style="
background:#1f2937;
border-left:4px solid #9ca3af;
padding:16px 18px;
border-radius:10px;
margin-top:20px;
">
<strong style="color:#f9fafb;">Final variable flow:</strong><br>
<code>X_kdd_raw</code> → <code>X_kdd_clean</code> → <code>X_train_normal_raw</code> → <code>X_train_normal_processed</code> → <code>autoencoder</code> → <code>reconstruction_results</code>
</div>

</div>
</div>