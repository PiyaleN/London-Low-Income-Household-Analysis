# London Low-Income Household Analysis

![R](https://img.shields.io/badge/R-4.x-blue)
![tidyverse](https://img.shields.io/badge/tidyverse-2.0-orange)
![ggplot2](https://img.shields.io/badge/ggplot2-3.4-green)

A statistical analysis of children living in low-income households across London's 32 boroughs from 2014 to 2021. Uses R and RMarkdown to clean ward-level data, compute descriptive statistics, visualise distributions, and test for significant change over the 8-year period.

---

## Key Findings

| Metric | 2014 | 2021 | Change |
|--------|------|------|--------|
| Mean children in low-income households | 528.32 | 603.87 | **+14.3%** |
| Welch t-test | — | — | **t = -4.02, p < 0.05** |

The increase from 2014 to 2021 is **statistically significant** — the null hypothesis (equal means) is rejected at the 95% confidence level.

---

## Analysis Pipeline

```
┌──────────────────┐     ┌──────────────────┐     ┌──────────────────┐     ┌──────────────────┐
│  Ward-Level Data │────▶│  Borough         │────▶│  Descriptive     │────▶│  Welch Two-      │
│  2014–2021       │     │  Aggregation     │     │  Statistics      │     │  Sample t-test   │
│  (CSV)           │     │  (dplyr)         │     │  + Viz (ggplot2) │     │  (2014 vs 2021)  │
└──────────────────┘     └──────────────────┘     └──────────────────┘     └──────────────────┘
```

### Methodology

1. **Data Aggregation** — 625 ward-level records grouped by borough, computing mean, SD, min, max per year
2. **Outlier Handling** — 5 boroughs with unusually low counts excluded (City of London, Kensington and Chelsea, Kingston upon Thames, Richmond upon Thames, Westminster)
3. **Visualisation** — Jitter plots with mean trend lines showing yearly distribution shifts
4. **Hypothesis Test** — Welch two-sample t-test (unequal variances) comparing 2014 vs 2021 means

---

## Results

### Yearly Distribution
![Yearly Distribution](yearly_distribution_plot.png)

### Borough Summary Statistics
![Borough Summary](borough_summary_statistics.png)

### t-Test Results
![t-Test Results](t_test_results.png)

---

## Project Structure

```
├── london_low_income_household_analysis.Rmd   # RMarkdown analysis
├── london_low_income_household_analysis.html  # Rendered HTML report
├── children_low_income_data.csv               # Input dataset (625 wards)
├── yearly_distribution_plot.png               # Distribution visualisation
├── borough_summary_statistics.png             # Borough-level stats
├── t_test_results.png                         # Hypothesis test output
└── README.md
```

---

## Installation & Reproduce

```bash
git clone https://github.com/Piyali-Narnaware/London-Low-Income-Household-Analysis.git
cd London-Low-Income-Household-Analysis
```

Open `london_low_income_household_analysis.Rmd` in RStudio and **Knit to HTML**, or run:

```r
rmarkdown::render("london_low_income_household_analysis.Rmd")
```

### Dependencies

```r
install.packages(c("tidyverse", "dplyr", "ggplot2", "knitr"))
```

---

## Dataset

- **Source**: London Datastore / Department for Work and Pensions
- **Scope**: Children in low-income households, London boroughs
- **Period**: 2014–2021
- **Granularity**: Ward-level (625 records)
- **Exclusions**: 5 boroughs removed due to suppressed/low counts
