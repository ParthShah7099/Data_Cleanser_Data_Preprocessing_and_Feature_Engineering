# 📊 FINDINGS — Data Cleanser
### Data Preprocessing & Feature Engineering — Summary Report

> *Project by THE PARTH SHAH | Red & White Skill Education, Surat*

---

## Dataset Overview

| Property | Value |
|---|---|
| Total Rows | 200 patients |
| Total Columns | 9 |
| Target Variable | `disease_risk` (0 = Low, 1 = High) |
| Missing Cells (before) | 99 |
| Missing Cells (after) | **0** |
| Rows after full cleaning | **179 / 200** |

---

## Part A — Missing Value Imputation: Results

| Column | Missing Count | Missing % | Best Strategy Applied | Reason |
|---|---|---|---|---|
| `age` | 18 | 9.0% | Mean | Normally distributed — mean is accurate |
| `gender` | 15 | 7.5% | Most Frequent | Categorical — mode is the only valid choice |
| `region` | 12 | 6.0% | Most Frequent | Categorical — mode is the only valid choice |
| `bmi` | 20 | 10.0% | MICE | Skewed + correlated with other columns |
| `cholesterol` | 18 | 9.0% | MICE | Correlated with glucose and BMI |
| `glucose` | 16 | 8.0% | MICE | Correlated with cholesterol and BMI |

### Imputation Strategy Comparison

| Strategy | Preserves Distribution | Handles Correlations | Verdict |
|---|---|---|---|
| Mean | ❌ No | ❌ No | Best only for normally distributed data |
| Median | Partially | ❌ No | Best when outliers present |
| Most Frequent | Partially | ❌ No | Only valid for categorical columns |
| Random Sample | ✅ Yes | ❌ No | Good when distribution matters most |
| Missing Indicator | N/A | N/A | Adds signal — use alongside imputation |
| KNN (k=5) | ✅ Yes | ✅ Approximate | Better than simple methods |
| **MICE** | ✅ **Best** | ✅ **Full** | **🏆 Most statistically rigorous** |

**Winner: MICE** — captures the biological correlations between age, BMI, cholesterol, and glucose that all univariate methods miss.

---

## Part B — Outlier Detection: Results

| Method | Column | Outliers Found | Values Detected | Rows Removed |
|---|---|---|---|---|
| Z-Score (\|Z\| > 3) | cholesterol | 3 | 420, 430, 8 mg/dL | 3 |
| Z-Score (\|Z\| > 3) | glucose | 3 | 380, 400, 350 mg/dL | 3 |
| IQR (1.5×IQR rule) | bmi | 7 | 55, 60.2, 58.5, 62, 3.1 + 2 | 7 |
| Percentile (1st–99th) | blood_pressure | 4 | 220, 230, 215 mmHg + 1 | 4 |
| **Winsorization (5th–95th)** | bmi | N/A | Capped, not removed | **0** |

### Outlier Method Comparison

| Method | Removes Rows | Robust to Skew | Best Use Case |
|---|---|---|---|
| Z-Score | ✅ Yes | ❌ No | Normally distributed columns |
| IQR | ✅ Yes | ✅ Yes | Any distribution — boxplot based |
| Percentile | ✅ Yes | ✅ Yes | Custom boundaries — highly flexible |
| **Winsorization** | ❌ **No** | ✅ Yes | **When data loss is unacceptable** |

**Best for accuracy: Z-Score** — mathematically rigorous, identifies true statistical anomalies.  
**Best for data preservation: Winsorization** — zero rows removed, extremes controlled.

---

## Part C — Before vs After Summary

| Metric | Before Cleaning | After Cleaning | Improvement |
|---|---|---|---|
| Total rows | 200 | 179 | Outlier rows removed |
| Missing cells | 99 | **0** | 100% resolved |
| Cholesterol max | 430 mg/dL | ~280 mg/dL | Within clinical range |
| Glucose max | 400 mg/dL | ~170 mg/dL | Within clinical range |
| BMI max | 62 | ~38 | Within biological range |
| Blood pressure max | 230 mmHg | ~165 mmHg | Within clinical range |
| ML-ready? | ❌ No | ✅ **Yes** | Ready for any classifier |

---

## Key Conclusions

**1. Imputation:** MICE outperforms all alternatives for healthcare data because medical variables are biologically correlated. A multivariate method that models these relationships during imputation produces the most statistically honest fill values.

**2. Outliers:** No single method fits all columns. Z-Score worked for normally distributed medical measurements. IQR handled skewed BMI. Percentile gave fine-grained control over blood pressure. Winsorization demonstrated that outlier treatment does not always require data deletion.

**3. Data quality:** The cleaning pipeline improved dataset usability from completely unusable (NaN-filled, outlier-distorted) to fully ML-ready — all column distributions are now within medically plausible ranges and suitable for downstream modelling.

---

*THE PARTH SHAH | AI/ML and Data Science | Red & White Skill Education, Surat | 2026*
