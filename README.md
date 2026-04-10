# Bendrix Company — Overhead Cost Analysis

**Author:** Md Abdullah Al Amin  
**LinkedIn:** [mdabdullah-amin](https://www.linkedin.com/in/mdabdullah-amin)  
**Tools:** Microsoft Excel (Data Analysis ToolPak — Regression)  
**Techniques:** Scatterplot analysis, Simple Linear Regression, Multiple Linear Regression

---

> 📄 **[View the full visual report (PDF)](Bendrix_Analysis_Report.pdf)** — Excel screenshots showing the data, scatterplots, and all regression outputs at a glance.

## Overview

This case study investigates what drives overhead costs at Bendrix Company, an automotive parts manufacturer. The factory manager wanted to better understand the behaviour of monthly overhead — which includes supervision, indirect labour, supplies, payroll taxes, overtime, depreciation, utilities, and maintenance — and determine whether production activity could statistically explain the variation in those costs.

Using a sample of 8 months of operational data, this analysis quantifies the relationship between overhead and two candidate drivers **Machine Hours** and **Production Runs** through scatterplot visualisation, two simple linear regressions, and a final multiple regression model that combines both predictors.

---

## Business Problem

Overhead costs contain both fixed and variable components, and the boundary between them is rarely clean. Fixed overhead tends to come from supervision, depreciation, and miscellaneous categories, while variable overhead is driven by indirect labour, supplies, payroll taxes, and overtime. The manager hypothesised that two variables could jointly explain monthly overhead variation:

- **Machine Hours** — a direct measure of production volume.
- **Production Runs** — the number of separate batches run in the month. Each new run requires machinery setup and downtime, which carries its own cost footprint independent of machine hours.

The question: can these two variables, individually or together, reliably explain overhead cost behaviour?

---

## Dataset

8 months of operational data with the following fields:

| Field | Description |
|---|---|
| Month | Month number (1–8) |
| Machine Hours | Total machine hours used during the month |
| Production Runs | Number of production runs completed during the month |
| Overhead | Total overhead cost for the month (USD) |

The raw data is in the `Bendrix Data` sheet of `Bendrix Data.xlsx`.

---

## Methodology

The analysis was conducted in four stages:

1. **Exploratory scatterplots** — three pairwise scatterplots to visually assess relationships between Overhead, Machine Hours, and Production Runs.
2. **Simple regression 1** — Overhead regressed on Machine Hours alone.
3. **Simple regression 2** — Overhead regressed on Production Runs alone.
4. **Multiple regression** — Overhead regressed on both Machine Hours and Production Runs jointly.

All regressions were run using Excel's Data Analysis ToolPak.

---

## Results

### Regression 1 — Overhead vs Machine Hours

| Statistic | Value |
|---|---|
| Multiple R | 0.4747 |
| R Square | 0.2253 |
| Adjusted R Square | 0.0962 |
| Standard Error | 11,630.35 |
| Observations | 8 |

| Predictor | Coefficient | Std. Error | t Stat | P-value |
|---|---:|---:|---:|---:|
| Intercept | 35,022.32 | 47,882.73 | 0.73 | 0.4921 |
| Machine Hours | 43.11 | 32.64 | 1.32 | 0.2347 |

**Equation:** `Overhead ≈ 35,022.32 + 43.11 × Machine Hours`

Machine Hours alone explains only **22.5%** of the variation in overhead. The p-value of 0.235 indicates the coefficient is not statistically significant — Machine Hours is a weak solo predictor.

---

### Regression 2 — Overhead vs Production Runs

| Statistic | Value |
|---|---|
| Multiple R | 0.8860 |
| R Square | 0.7850 |
| Adjusted R Square | 0.7491 |
| Standard Error | 6,127.31 |
| Observations | 8 |

| Predictor | Coefficient | Std. Error | t Stat | P-value |
|---|---:|---:|---:|---:|
| Intercept | 60,624.09 | 8,282.82 | 7.32 | 0.0003 |
| Production Runs | 1,138.11 | 243.18 | 4.68 | 0.0034 |

**Equation:** `Overhead ≈ 60,624.09 + 1,138.11 × Production Runs`

Production Runs alone explains **78.5%** of overhead variation, with a highly significant coefficient (p = 0.003). Each additional production run is associated with roughly **$1,138** of added overhead — a plausible reflection of setup and changeover costs.

---

### Regression 3 — Multiple Regression (Machine Hours + Production Runs)

| Statistic | Value |
|---|---|
| Multiple R | 0.9710 |
| R Square | 0.9428 |
| Adjusted R Square | 0.9200 |
| Standard Error | 3,460.68 |
| Observations | 8 |

| Predictor | Coefficient | Std. Error | t Stat | P-value |
|---|---:|---:|---:|---:|
| Intercept | 9,163.87 | 14,616.86 | 0.63 | 0.5582 |
| Machine Hours | 36.23 | 9.75 | 3.72 | 0.0138 |
| Production Runs | 1,092.47 | 137.89 | 7.92 | 0.0005 |

**Equation:** `Overhead ≈ 9,163.87 + 36.23 × Machine Hours + 1,092.47 × Production Runs`

**ANOVA:** F = 41.24, Significance F = 0.00078 — the overall model is highly significant.

Combining both predictors jumps R² to **94.3%**, and critically, **Machine Hours now becomes statistically significant** (p = 0.014) once Production Runs is controlled for. This is the key insight of the analysis.

---

## Interpretation and Insights

1. **Production Runs is the dominant driver of overhead.** On its own it explains nearly 79% of the variation, consistent with the idea that setup, changeover, and batch-level activities carry substantial fixed costs per run (~$1,092 per additional run in the full model).

2. **Machine Hours matters — but only once Production Runs is accounted for.** In the simple regression, Machine Hours looked like a weak predictor (p = 0.235). In the multiple regression it becomes clearly significant (p = 0.014) with a coefficient of ~$36.23 per additional machine hour. This is a textbook example of why single-variable analysis can mislead: Machine Hours and Production Runs partially correlate, and only by controlling for one can the true effect of the other be isolated.

3. **The combined model is substantially stronger than either simple regression.** R² climbs from 0.23 and 0.79 to 0.94, and the standard error drops from 11,630 (Regression 1) to 3,461 (Regression 3) — a nearly 70% reduction in unexplained variation.

4. **The manager's original intuition was correct.** Both variables contribute to overhead in different ways: Machine Hours captures the variable cost of actual production activity, while Production Runs captures the fixed, batch-level setup cost. Both are needed to explain overhead behaviour.

---

## Conclusion

Multiple regression provides a far more convincing explanation of overhead cost behaviour at Bendrix than either simple regression alone. The final model — with 94.3% of variance explained and both predictors significant — supports a cost structure where overhead is driven jointly by production volume (Machine Hours) and production complexity (Production Runs). For cost forecasting or budgeting purposes, the two-variable model should be preferred.

---

## Repository Contents

| File | Description |
|---|---|
| `README.md` | This report |
| `Bendrix Data.xlsx` | Raw data, scatterplots, and three regression outputs |
| `Bendrix_Analysis_Report.pdf` | Visual report with Excel screenshots (data, scatterplots, and regression results) |
