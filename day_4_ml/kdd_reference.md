<div style="
background:#111827;
color:#e5e7eb;
border-radius:16px;
font-family:Arial, sans-serif;
line-height:1.6;
border:1px solid #374151;
overflow:hidden;
">

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
Quick Reference Map
</div>

<h1 style="
color:#f9fafb;
margin:0;
font-size:25px;
font-weight:800;
line-height:1.25;
">
KDD Cup 1999 Autoencoder Workflow
</h1>

<p style="
color:#9ca3af;
margin:10px 0 0 0;
font-size:14px;
">
Prepared by <strong style="color:#d1d5db;">Ruturaj Mokashi</strong>
</p>
</div>

<div style="padding:28px;">

<h2 style="color:#f3f4f6; font-size:18px; border-left:4px solid #6b7280; padding-left:12px;">
1. Data Loading
</h2>

<pre style="
background:#0f172a;
color:#e5e7eb;
padding:16px;
border-radius:10px;
border:1px solid #374151;
overflow:auto;
">
fetch_kddcup99()
        ↓
X_kdd_raw     = raw feature columns
y_kdd_raw     = raw target labels
</pre>

<h2 style="color:#f3f4f6; font-size:18px; border-left:4px solid #6b7280; padding-left:12px;">
2. Target Preparation
</h2>

<pre style="
background:#0f172a;
color:#e5e7eb;
padding:16px;
border-radius:10px;
border:1px solid #374151;
overflow:auto;
">
y_kdd_raw
        ↓
y_kdd_clean
        ↓
y_kdd_binary

0 = Normal
1 = Anomaly
</pre>

<h2 style="color:#f3f4f6; font-size:18px; border-left:4px solid #6b7280; padding-left:12px;">
3. Feature Type Correction
</h2>

<pre style="
background:#0f172a;
color:#e5e7eb;
padding:16px;
border-radius:10px;
border:1px solid #374151;
overflow:auto;
">
X_kdd_raw
        ↓
X_kdd_clean

corrected_numerical_columns      = 38 columns
corrected_categorical_columns    = 3 columns
</pre>

<p>
The true categorical columns were:
</p>

<ul>
<li><code>protocol_type</code></li>
<li><code>service</code></li>
<li><code>flag</code></li>
</ul>

<h2 style="color:#f3f4f6; font-size:18px; border-left:4px solid #6b7280; padding-left:12px;">
4. Train/Test Split
</h2>

<pre style="
background:#0f172a;
color:#e5e7eb;
padding:16px;
border-radius:10px;
border:1px solid #374151;
overflow:auto;
">
X_kdd_clean + y_kdd_binary
        ↓
X_train_raw, X_test_raw


y_train, y_test
        ↓
X_train_normal_raw

Only normal rows are used for Autoencoder training.
</pre>

<h2 style="color:#f3f4f6; font-size:18px; border-left:4px solid #6b7280; padding-left:12px;">
5. Preprocessing
</h2>

<pre style="
background:#0f172a;
color:#e5e7eb;
padding:16px;
border-radius:10px;
border:1px solid #374151;
overflow:auto;
">
X_train_normal_raw
        ↓
preprocessor.fit()

X_train_normal_raw  → X_train_normal_processed
X_train_raw         → X_train_processed
X_test_raw          → X_test_processed
</pre>

<table style="width:100%; border-collapse:collapse; color:#e5e7eb; margin:18px 0;">
<tr>
<th style="text-align:left; padding:8px; border-bottom:1px solid #4b5563;">Processed Data</th>
<th style="text-align:left; padding:8px; border-bottom:1px solid #4b5563;">Shape</th>
</tr>
<tr>
<td style="padding:8px;">Normal training data</td>
<td style="padding:8px;"><strong>77,822 × 74</strong></td>
</tr>
<tr>
<td style="padding:8px;">Full training data</td>
<td style="padding:8px;"><strong>395,216 × 74</strong></td>
</tr>
<tr>
<td style="padding:8px;">Test data</td>
<td style="padding:8px;"><strong>98,805 × 74</strong></td>
</tr>
</table>

<h2 style="color:#f3f4f6; font-size:18px; border-left:4px solid #6b7280; padding-left:12px;">
6. Autoencoder Model
</h2>

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
The Autoencoder was trained using:
</p>

<pre style="
background:#0f172a;
color:#e5e7eb;
padding:16px;
border-radius:10px;
border:1px solid #374151;
overflow:auto;
">
autoencoder.fit(
    X_train_normal_processed,
    X_train_normal_processed
)
</pre>

<h2 style="color:#f3f4f6; font-size:18px; border-left:4px solid #6b7280; padding-left:12px;">
7. Reconstruction Error
</h2>

<pre style="
background:#0f172a;
color:#e5e7eb;
padding:16px;
border-radius:10px;
border:1px solid #374151;
overflow:auto;
">
X_test_processed
        ↓
autoencoder.predict()
        ↓
X_test_reconstructed
        ↓
test_reconstruction_error
        ↓
reconstruction_results
</pre>

<p>
Reconstruction error became the anomaly score.
</p>

<ul>
<li>Low error = likely normal</li>
<li>High error = likely anomaly</li>
</ul>

<h2 style="color:#f3f4f6; font-size:18px; border-left:4px solid #6b7280; padding-left:12px;">
8. Threshold and Prediction
</h2>

<pre style="
background:#0f172a;
color:#e5e7eb;
padding:16px;
border-radius:10px;
border:1px solid #374151;
overflow:auto;
">
train_normal_reconstruction_error
        ↓
95th percentile threshold
        ↓
reconstruction_results["predicted_label"]

0 = Predicted Normal
1 = Predicted Anomaly
</pre>

<h2 style="color:#f3f4f6; font-size:18px; border-left:4px solid #6b7280; padding-left:12px;">
9. Final Comparison
</h2>

<table style="width:100%; border-collapse:collapse; color:#e5e7eb; margin:18px 0;">
<tr>
<th style="text-align:left; padding:8px; border-bottom:1px solid #4b5563;">Model</th>
<th style="text-align:left; padding:8px; border-bottom:1px solid #4b5563;">F1-score</th>
<th style="text-align:left; padding:8px; border-bottom:1px solid #4b5563;">Missed Attacks</th>
</tr>
<tr>
<td style="padding:8px;">Autoencoder</td>
<td style="padding:8px;"><strong>0.9931</strong></td>
<td style="padding:8px;"><strong>125</strong></td>
</tr>
<tr>
<td style="padding:8px;">Isolation Forest</td>
<td style="padding:8px;"><strong>0.9894</strong></td>
<td style="padding:8px;"><strong>773</strong></td>
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
Final Result
</h2>

<p style="margin-bottom:0;">
The <strong>Autoencoder</strong> was the stronger model because it achieved the higher F1-score and missed far fewer attacks than Isolation Forest.
</p>

</div>

</div>
</div>