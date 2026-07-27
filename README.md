# Analysis of Political Violence and Protest Events in Turkey (2016–2023)

Event-level statistical analysis of **22,110 recorded political violence and protest events** in Turkey, using data from the Armed Conflict Location & Event Data Project (ACLED). The project covers the full pipeline: raw data cleaning and event-level restructuring, exploratory data analysis, formal hypothesis testing, and regression modeling with robust inference.

> Course project for **STAT250 — Applied Statistics**, Middle East Technical University (METU), Department of Statistics.

---

## Overview

The raw ACLED dataset contained **32,447 rows and 31 variables**, with some events split across multiple rows. After cleaning, deduplication, and event-level restructuring, the final analysis dataset contained **22,110 unique events and 65 variables** covering 2016–2023. Because the data is observational, all results are reported as **associations, not causal effects**.

## Research Questions & Methods

| # | Research Question | Statistical Method |
|---|-------------------|--------------------|
| RQ1 | Are protests the majority of events, and is fatality status associated with event type? | One-sample proportion z-test · Chi-square test of independence (Cramér's V) |
| RQ2 | Do violent events have a higher fatal-event rate than non-violent events? | Two-proportion z-test |
| RQ3 | Are more severe events associated with broader reporting coverage? | Levene's test · Welch's two-sample t-test · Mann–Whitney U (sensitivity check) |
| RQ4 | Do event types differ in their population context? | Welch's ANOVA · Pairwise comparisons with Holm correction |
| RQ5 | Which variables are associated with event severity? | Multiple linear regression with **HC3 robust standard errors** · Breusch–Pagan · Jarque–Bera · VIF |

## Key Findings

- **Protests** made up ~57.8% of all recorded events — a statistically significant majority (z = 23.23, p < 0.001).
- Fatality status was **strongly associated** with event type (χ²(5) = 9292.7, p < 0.001; Cramér's V = 0.648).
- Violent events had a ~43.2% fatal-event rate vs. ~0.05% for non-violent events.
- In the regression model, **violent-event classification** was the most prominent predictor of reported severity. Heteroskedasticity and non-normal residuals were detected and handled with HC3 robust standard errors.

## Data Cleaning Highlights

- Event-level deduplication (32,447 → 22,110 unique events).
- Type standardization for IDs, dates, and numeric fields.
- Missing-value handling per the ACLED Codebook (fatalities → 0; `source_scale` → source-specific mode, then global mode).
- Derived variables: `fatal_event`, `violent_event`, `actor_count`, `source_count`, `population_for_analysis`, and log transformations to address right-skew.

## Repository Structure

```
├── Stat250_Project_Group_11.ipynb      # Full analysis notebook
├── Stat_250_Project_Report_Group_11.pdf # Written report
└── README.md
```

## Tech Stack

`Python` · `pandas` · `NumPy` · `SciPy` · `statsmodels` · `matplotlib` · `geopandas`

## How to Run

```bash
git clone https://github.com/hasanakkaya0/turkey-political-violence-analysis.git
cd turkey-political-violence-analysis
pip install pandas numpy scipy statsmodels matplotlib geopandas
jupyter notebook Stat250_Project_Group_11.ipynb
```

> The raw ACLED dataset is not redistributed here. Access it via the [ACLED Data Export Tool](https://acleddata.com/).

## Authors

Hasan Akkaya · Aslı Ceren Aksu · Ahmet Genç

## License

Released under the MIT License. ACLED data is subject to [ACLED's terms of use](https://acleddata.com/terms-of-use/).
