# Tag 4 Outlier, Anomaly

# Hauptmaterial

## Vorlesung

html slides

https://medium.com/dataman-in-ai/handbook-of-anomaly-detection-10-cluster-based-local-outlier-factor-cblof-1c339ae2056a

https://medium.com/@abhaysingh71711/the-impact-of-outliers-on-data-when-to-remove-and-when-to-retain-fb6e474ddbd8

**When to drop or keep outliers?**

I believe that the dropping outlier is always a harsh step and should be taken only in extreme conditions when we’re very sure that the **outlier is due to a measurement error**, which we generally do not know while doing analysis.

Sometimes outliers indicate a mistake in data collection. Other times, though, they can influence a data set, so it’s important to keep them to better understand the dataset in the big picture.

👉 **Inter-Quartile Range (IQR):** The IQR is the difference between the 75th and 25th percentile. The IQR is more resistant to outliers. 

👉**Range:** Most affected by the outliers since it is the difference b/w the max and min value present in the dataset.

## 

# Themen

**Verstehen wieso Ausreisser problematisch sein können und wann sie entfernt werden sollen**

**Algorithmen für die Ausreissererkennung kennenlernen**

# Zusatzmaterial

## ABOD

https://www.dbs.ifi.lmu.de/Publikationen/Papers/KDD2008.pdf

## Loop

https://www.dbs.ifi.lmu.de/Publikationen/Papers/LoOP1649.pdf

### Isolation Forest

https://www.lamda.nju.edu.cn/publication/icdm08b.pdf

Paper:

https://www.researchgate.net/profile/Fei-Tony-Liu/publication/224384174_Isolation_Forest/links/5bbd5c0ca6fdcc9552dd04f0/Isolation-Forest.pdf?origin=publication_detail&_tp=eyJjb250ZXh0Ijp7ImZpcnN0UGFnZSI6InB1YmxpY2F0aW9uIiwicGFnZSI6InB1YmxpY2F0aW9uRG93bmxvYWQiLCJwcmV2aW91c1BhZ2UiOiJwdWJsaWNhdGlvbiJ9fQ

### CBLOF

https://medium.com/dataman-in-ai/handbook-of-anomaly-detection-10-cluster-based-local-outlier-factor-cblof-1c339ae2056a

https://statisticsbyjim.com/basics/remove-outliers/

What do you do when you can’t legitimately remove outliers, but they violate the assumptions of your statistical analysis? You want to include them but don’t want them to distort the results. Fortunately, there are various statistical analyses up to the task. Here are several options you can try.

[Nonparametric hypothesis tests are robust to outliers](https://statisticsbyjim.com/hypothesis-testing/nonparametric-parametric-tests/). For these alternatives to the more common parametric tests, outliers won’t necessarily violate their assumptions or distort their results.

In regression analysis, you can try transforming your data or using a robust regression analysis available in some statistical packages.

Finally, [bootstrapping techniques](https://statisticsbyjim.com/hypothesis-testing/bootstrapping/) use the sample data as they are and don’t make assumptions about distributions.

These types of analyses allow you to capture the full variability of your dataset without violating assumptions and skewing results.