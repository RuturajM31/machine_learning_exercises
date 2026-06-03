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
KDD Cup 1999 — Concept Summary
</div>

<h1 style="
color:#f9fafb;
margin:0;
font-size:26px;
font-weight:800;
line-height:1.25;
">
Autoencoder Anomaly Detection
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
Project Goal
</h2>

<p>
The goal of this project was to detect suspicious network connections using an <strong>Autoencoder</strong>.
</p>

<p>
The KDD Cup 1999 dataset contains network connection records. Each row represents one network connection. Some rows are normal connections, while others are attack-like connections.
</p>

<div style="
background:#1f2937;
border-left:4px solid #9ca3af;
padding:16px 18px;
border-radius:10px;
margin:20px 0;
">
<strong style="color:#f9fafb;">Simple idea:</strong><br>
Train the Autoencoder only on normal network traffic. Then use reconstruction error to identify suspicious rows.
</div>

<pre style="
background:#0f172a;
color:#e5e7eb;
padding:16px;
border-radius:10px;
border:1px solid #374151;
overflow:auto;
">
Normal network traffic
        ↓
Autoencoder learns normal behavior
        ↓
Test data is reconstructed
        ↓
Reconstruction error is calculated
        ↓
High reconstruction error = possible anomaly / attack
</pre>

<h2 style="color:#f3f4f6; font-size:19px; border-left:4px solid #6b7280; padding-left:12px;">
Why Autoencoder?
</h2>

<p>
An Autoencoder is useful for anomaly detection because it learns how normal data should look.
</p>

<ul>
<li>Normal rows should be reconstructed well.</li>
<li>Anomaly rows should be reconstructed poorly.</li>
<li>Poor reconstruction creates high reconstruction error.</li>
<li>High reconstruction error becomes the anomaly score.</li>
</ul>

<h2 style="color:#f3f4f6; font-size:19px; border-left:4px solid #6b7280; padding-left:12px;">
Dataset Understanding
</h2>

<table style="width:100%; border-collapse:collapse; color:#f9fafb; margin:18px 0; font-size:14px;">
<tr style="background:#1f2937;">
<th style="text-align:left; padding:10px; border:1px solid #4b5563; color:#ffffff;">Item</th>
<th style="text-align:left; padding:10px; border:1px solid #4b5563; color:#ffffff;">Value</th>
</tr>
<tr>
<td style="padding:10px; border:1px solid #4b5563; color:#e5e7eb;">Total rows</td>
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;">494,021</td>
</tr>
<tr style="background:#0f172a;">
<td style="padding:10px; border:1px solid #4b5563; color:#e5e7eb;">Original feature columns</td>
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;">41</td>
</tr>
<tr>
<td style="padding:10px; border:1px solid #4b5563; color:#e5e7eb;">Normal rows</td>
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;">97,278</td>
</tr>
<tr style="background:#0f172a;">
<td style="padding:10px; border:1px solid #4b5563; color:#e5e7eb;">Anomaly rows</td>
<td style="padding:10px; border:1px solid #4b5563; color:#ffffff; font-weight:700;">396,743</td>
</tr>
</table>

<div style="
background:#1f2937;
border-left:4px solid #9ca3af;
padding:16px 18px;
border-radius:10px;
margin-top:20px;
">
<strong style="color:#f9fafb;">Main learning:</strong><br>
This was a network security anomaly detection project. 

The Autoencoder learned normal network behavior and used reconstruction error to detect attack-like traffic.
</div>

</div>
</div>