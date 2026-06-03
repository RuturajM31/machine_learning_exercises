<div style="
background:#0f172a;
color:#e5e7eb;
padding:28px;
border-radius:18px;
font-family:Arial, sans-serif;
line-height:1.65;
border:1px solid #334155;
">

<h1 style="color:#f8fafc; margin-top:0;">Quick Reference — Outlier Detection Work Completed Today</h1>

<p style="color:#cbd5e1;">
A short summary of the full outlier detection workflow completed on the Industrial Equipment Monitoring dataset.
</p>

<hr style="border:0; border-top:1px solid #334155; margin:24px 0;">

<h2 style="color:#38bdf8;">1. Data Preparation</h2>
<ul>
<li>Loaded the Industrial Equipment Monitoring dataset.</li>
<li>Selected the main sensor columns: <code>temperature</code>, <code>pressure</code>, <code>vibration</code>, <code>humidity</code>.</li>
<li>Scaled the sensor columns using <code>StandardScaler</code>.</li>
<li>Used <code>faulty</code> only for final evaluation, not for training.</li>
</ul>

<h2 style="color:#38bdf8;">2. Z-Score Outlier Detection</h2>
<ul>
<li>Calculated Z-Scores for each sensor column.</li>
<li>Marked rows as outliers when any sensor had <code>|Z-Score| &gt; 3</code>.</li>
<li>Detected <strong style="color:#facc15;">467 outlier rows</strong>.</li>
<li>Built charts and compared before/after statistics.</li>
<li>Z-Score became the final best-performing algorithm.</li>
</ul>

<h2 style="color:#38bdf8;">3. Isolation Forest</h2>
<ul>
<li>Trained Isolation Forest on scaled sensor data.</li>
<li>Used <code>contamination = 0.05</code>.</li>
<li>Detected <strong style="color:#facc15;">384 outlier rows</strong>.</li>
<li>Compared results with LOF and other algorithms.</li>
</ul>

<h2 style="color:#38bdf8;">4. LOF — Local Outlier Factor</h2>
<ul>
<li>Trained LOF on scaled sensor data.</li>
<li>Used <code>contamination = 0.05</code>.</li>
<li>Detected <strong style="color:#facc15;">384 outlier rows</strong>.</li>
<li>Found that LOF and Isolation Forest detected mostly different rows.</li>
</ul>

<h2 style="color:#38bdf8;">5. PCA Visualization</h2>
<ul>
<li>Reduced four sensor columns into <code>PC1</code> and <code>PC2</code>.</li>
<li>PC1 + PC2 explained <strong style="color:#facc15;">53.41%</strong> of sensor variation.</li>
<li>Used PCA scatter plots to visually inspect outlier locations.</li>
</ul>

<h2 style="color:#38bdf8;">6. Jaccard Comparison</h2>
<ul>
<li>Compared overlap between Isolation Forest and LOF.</li>
<li>Shared outliers: <strong style="color:#facc15;">32</strong>.</li>
<li>Jaccard score: <strong style="color:#facc15;">0.0435</strong>.</li>
<li>Conclusion: Isolation Forest and LOF detected very different outlier rows.</li>
</ul>

<h2 style="color:#38bdf8;">7. ABOD — Angle-Based Outlier Detection</h2>
<ul>
<li>Installed required packages using Conda.</li>
<li>Trained ABOD on scaled sensor data.</li>
<li>Detected <strong style="color:#facc15;">384 outlier rows</strong>.</li>
<li>Created PCA chart for ABOD outliers.</li>
</ul>

<h2 style="color:#38bdf8;">8. CBLOF — Cluster-Based Local Outlier Factor</h2>
<ul>
<li>Trained CBLOF on scaled sensor data.</li>
<li>Detected <strong style="color:#facc15;">384 outlier rows</strong>.</li>
<li>Created PCA chart for CBLOF outliers.</li>
<li>CBLOF was one of the stronger algorithms.</li>
</ul>

<h2 style="color:#38bdf8;">9. LoOP — Local Outlier Probability</h2>
<ul>
<li>Calculated LoOP anomaly scores.</li>
<li>Used the top 5% highest LoOP scores as outliers.</li>
<li>Threshold used: <code>0.5408</code>.</li>
<li>Detected <strong style="color:#facc15;">384 outlier rows</strong>.</li>
<li>Created LoOP score distribution and PCA charts.</li>
</ul>

<h2 style="color:#38bdf8;">10. Agreement Between ABOD, CBLOF, and LoOP</h2>
<ul>
<li>Normal by all three algorithms: <strong style="color:#facc15;">6,870 rows</strong>.</li>
<li>Flagged by 1 algorithm: <strong style="color:#facc15;">471 rows</strong>.</li>
<li>Flagged by 2 algorithms: <strong style="color:#facc15;">312 rows</strong>.</li>
<li>Flagged by ABOD, CBLOF, and LoOP: <strong style="color:#facc15;">19 rows</strong>.</li>
<li>The 19 shared rows are high-priority anomaly candidates.</li>
</ul>

<h2 style="color:#38bdf8;">11. Pairwise Agreement Heatmap</h2>
<ul>
<li>ABOD vs CBLOF Jaccard score: <strong style="color:#facc15;">0.4463</strong>.</li>
<li>ABOD vs LoOP Jaccard score: <strong style="color:#facc15;">0.1725</strong>.</li>
<li>CBLOF vs LoOP Jaccard score: <strong style="color:#facc15;">0.0254</strong>.</li>
<li>ABOD and CBLOF agreed the most.</li>
<li>LoOP detected a different type of anomaly pattern.</li>
</ul>

<h2 style="color:#38bdf8;">12. Master Algorithm Comparison</h2>
<ul>
<li>Compared all algorithms against the <code>faulty</code> label.</li>
<li>Metrics used: Precision, Recall, and F1-score.</li>
<li>Algorithms compared: Z-Score, Isolation Forest, LOF, ABOD, CBLOF, and LoOP.</li>
</ul>

<div style="
background:#111827;
border:1px solid #facc15;
border-radius:14px;
padding:20px;
margin-top:24px;
">

<h2 style="color:#facc15; margin-top:0;">Final Winner — Ultimate Hero: Z-Score</h2>

<ul>
<li>Precision: <strong>0.9914</strong></li>
<li>Recall: <strong>0.6037</strong></li>
<li>F1-score: <strong>0.7504</strong></li>
</ul>

<p>
<strong>Final conclusion:</strong> For this Industrial Equipment dataset, Z-Score performed best because faulty rows were often linked to extreme sensor values.
</p>

</div>

</div>