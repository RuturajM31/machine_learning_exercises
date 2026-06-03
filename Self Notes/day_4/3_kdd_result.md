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
KDD Cup 1999 — Final Result Summary
</div>

<h1 style="
color:#f9fafb;
margin:0;
font-size:26px;
font-weight:800;
line-height:1.25;
">
Autoencoder vs Isolation Forest
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
Why We Compared These Models
</h2>

<p>
After building the Autoencoder, we compared it with Isolation Forest.
</p>

<p>
This gave us a comparison between:
</p>

<ul>
<li>Autoencoder — neural-network-based anomaly detection</li>
<li>Isolation Forest— traditional tree-based anomaly detection</li>
</ul>

<p>
Both models were trained on normal traffic and evaluated on the same test set.
</p>

<h2 style="color:#f3f4f6; font-size:19px; border-left:4px solid #6b7280; padding-left:12px;">
Model Performance
</h2>

<table style="width:100%; border-collapse:collapse; color:#f9fafb; margin:18px 0; font-size:14px;">
<tr style="background:#1f2937;">
<th style="text-align:left; padding:10px; border:1px solid #4b5563; color:#ffffff;">Model</th>
<th style="text-align:left; padding:10px; border:1px solid #4b5563; color:#ffffff;">Precision</th>
<th style="text-align:left; padding:10px; border:1px solid #4b5563; color:#ffffff;">Recall</th>
<th style="text-align:left; padding:10px; border:1px solid #4b5563; color:#ffffff;">F1-score</th>
<th style="text-align:left; padding:10px; border:1px solid #4b5563; color:#ffffff;">Accuracy</th>
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

<h2 style="color:#f3f4f6; font-size:19px; border-left:4px solid #6b7280; padding-left:12px;">
Security Error Comparison
</h2>

<table style="width:100%; border-collapse:collapse; color:#f9fafb; margin:18px 0; font-size:14px;">
<tr style="background:#1f2937;">
<th style="text-align:left; padding:10px; border:1px solid #4b5563; color:#ffffff;">Model</th>
<th style="text-align:left; padding:10px; border:1px solid #4b5563; color:#ffffff;">False Alarms</th>
<th style="text-align:left; padding:10px; border:1px solid #4b5563; color:#ffffff;">Missed Attacks</th>
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
border-left:4px solid #9ca3af;
padding:16px 18px;
border-radius:10px;
margin:20px 0;
">
<strong style="color:#f9fafb;">Security interpretation:</strong><br>
In network security, missed attacks are more dangerous than false alarms. Autoencoder missed only 125 attacks, while Isolation Forest missed 773 attacks.
</div>

<h2 style="color:#f3f4f6; font-size:19px; border-left:4px solid #6b7280; padding-left:12px;">
Final Winner
</h2>

<div style="
background:#1f2937;
border:1px solid #4b5563;
border-left:4px solid #9ca3af;
padding:18px;
border-radius:12px;
margin-top:20px;
">

<h2 style="
color:#f9fafb;
font-size:20px;
margin-top:0;
">
Autoencoder Wins
</h2>

<p>
The Autoencoder performed better overall because it achieved:
</p>

<ul>
<li>higher recall</li>
<li>higher F1-score</li>
<li>higher accuracy</li>
<li>far fewer missed attacks</li>
</ul>

<p style="margin-bottom:0;">
The final result shows that the Autoencoder is the stronger model for this KDD Cup 1999 anomaly detection task.
</p>

</div>

</div>
</div>