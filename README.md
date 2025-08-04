# 📊 Vanguard A/B Test Analysis — README Summary

This README documents the full pipeline across four notebooks (`data_cleaning.ipynb`, `eda.ipynb`, `kpi.ipynb`, `statistical_analysis.ipynb`) used to analyze user behavior, conversion performance, and demographic patterns in a controlled A/B experiment. All code, logic, and visualizations were crafted for clarity, reproducibility, and stakeholder usability.

---

## 📁 1. Data Cleaning & Structuring (`data_cleaning.ipynb`)

Prepares raw experiment data for downstream analysis by applying rigorous filtering, formatting, and reshaping.

- Loaded merged datasets containing user events, variation labels, and demographic fields.
- Standardized field names, ensured datetime consistency (`date_time`), and removed invalid records (e.g. `variation = 'unknown'`).
- Reshaped wide-format error tables into long format for visualization.
- Subsetted clean data into thematic subsets (`base`, `filtered`, `merged_sorted`) for KPIs and funnel tracking.

---

## 🧭 2. Exploratory Data Analysis (`eda.ipynb`)

Explores initial distribution patterns across key variables with clear, variation-aware plots.

### 🎨 Visuals Produced:
- **Age Distribution** by `variation`, using KDE-smoothed histograms.
- **Tenure Distribution** in years, group-labeled and stylized for presentation clarity.
- **Gender Distribution** using `countplot()` with control/test overlays.

### 📌 Notes:
- Excluded `unknown` categories in variation and gender for meaningful comparisons.
- Used dark-themed aesthetics (`black` background, `viridis` palettes, white labels) to support integration with dashboard.
- Combined multi-variable plots for demographic skew detection across experimental groups.

---

## 📈 3. KPI Calculations & Funnel Progression (`kpi.ipynb`)

Core metrics derived and visualized to evaluate performance of `test` vs `control` groups.

### ✅ Completion Rate:
- Defined starters (`process_step == 'start'`) and completions (`process_step == 'confirm'`) per variation.
- Calculated conversion rates with rounding and displayed:
  - **Control:** 60.08%
  - **Test:** 67.88%

### ⏱️ Time per Step:
- Calculated `step_duration` via timestamp diff by visitor.
- Converted to minutes and filtered out sessions > 1 hour.
- Aggregated average time per `process_step` and visualized bar chart (`white` vs `lightseagreen` bars).

### 🚶 Funnel Conversion:
- Counted % of users progressing through each step (`start → confirm`) per variation group.
- Normalized and plotted funnel stages with annotated bar labels for drop-off detection.

### ⚠️ Error Rate Enrichment:
- Merged computed `error_rate_by_step` onto main `df`, indexed by `process_step` and `variation`.
- Created enriched CSV for further dashboard integration.

---

## 🧪 4. Statistical Analysis (`statistical_analysis.ipynb`)

Tests confirm whether observed performance uplift is statistically and business-significant.

### 📐 Two-Tailed Z-Test:
- Compared completion rates between `test` and `control`.
- Result: **+7.80% uplift** → **Statistically significant (p < 0.05)** → *Reject H₀*

### 🎯 One-Tailed Test with Threshold:
- Minimum detectable effect (MDE): **+5% uplift**
- Used `proportions_ztest()` with `alternative='larger'`
- Result: uplift exceeds threshold → *Business impact confirmed*

### 📊 Completion Rate Visualization:
- Bar chart with annotated uplift and red threshold line.
- Designed with stakeholder readability in mind (dark background, bold labels, lime callouts).

### 🧬 Demographic Balance Checks:
- **Age:**
  - Extracted and compared using Welch’s t-test.
  - Visual and descriptive summary added.
- **Tenure:**
  - Same statistical procedure and summary.
  - Results confirm adequate group balance or help interpret test results with context.

---

## 📦 Final Outputs

- Enriched datasets:
  - `vanguard_with_avg_step_duration.csv`
  - `vanguard_with_error_rate.csv`
- Visuals and KPIs styled for dashboard-ready integration.
- All sections documented and methodologically aligned with stakeholder reporting needs.

---

## 🧰 Tools Used

- **Python (pandas, seaborn, matplotlib, statsmodels, scipy)** for data manipulation, statistical analysis, and custom visualization
- **Tableau** for interactive visualizations of KPIs, error rates, and demographic comparisons

---

## 🔗 Sources & References

- [📊 Final Presentation ](https://www.canva.com/design/DAGuR0n-g4o/sDLRjR5PrQCR7owALcSukQ/edit): project summary, methodology, key findings, and recommendations  

# vanguard_project
