# Cross-National Variation in LGBT+ Rights Support in the EU

**Survey Research Methodology II**  
Paloma Navarro, Anita Di Gennaro, Gaspar Andrés Vigneaux Poirot, Sude Boz

---

## Overview

This project investigates cross-national variation in support for LGBT+ equal rights across 28 EU member states, using data from the Special Eurobarometer 493 (2019). We focus on why support increased in some countries between 2015 and 2019 while declining in 9 others (Bulgaria, Czech Republic, Denmark, Ireland, Hungary, Italy, Croatia, Malta, and Slovakia).

Support ranges from around 31% in Slovakia to 98% in Sweden — a spread of nearly 70 percentage points — motivating a multilevel analytical framework that accounts for both individual and country-level factors.

---

## Research Question

> Why does cross-national variation in LGBT+ rights support persist across EU countries, and what individual and country-level factors explain it?

---

## Data

### Micro Data — Special Eurobarometer 493
- Wave 91.4, fielded 9–25 May 2019
- 28 EU member states, N = 27,438
- Key variables: socio-demographics, political orientation, religion, minority identity, discrimination experience, LGBT+-specific attitudes

### Macro Data — V-Dem Dataset (Maerz et al., 2025)
- Filtered to 2019, matched via ISO2 country codes
- Key variables: LGBT political power (`v2pepwrort`), freedom of expression, political polarisation, online hate speech, educational equality, GDP per capita

---

## Methods

We use **binomial Generalised Linear Mixed Models (GLMMs)** estimated with the `lme4` package in R, following a three-step multilevel approach:

1. **Null model** — decomposes total variance between individual and country levels (VPC = 0.30)
2. **Model 2** — adds individual-level predictors as fixed effects (VPC = 0.18)
3. **Model 3** — adds country-level V-Dem macro indicators (VPC = 0.09)

Country-specific logistic regressions are also estimated to visualise heterogeneity across the 28 countries before formal multilevel modelling.

---

## Key Findings

- **30%** of total variance in LGBT+ support is attributable to country-level differences
- **Having LGBT+ friends** is the strongest individual-level predictor
- **LGBT political power** is the only significant country-level predictor — GDP, freedom of expression, polarisation, and educational equality did not reach significance
- Spain and Sweden show the highest baseline support; Slovakia and Estonia the lowest
- Contact (interpersonal) and institutional representation (political power) operate independently and accumulate

---

## Repository Structure

```
├── Challenge_Final.qmd        # Main analysis file (Quarto)
├── Challenge_Report.qmd       # Report file (Quarto)
├── merged_data.csv            # Raw merged dataset
├── merged_data_dummy.csv      # Processed dataset with dummy variables
├── mod_null.rds               # Saved null model
├── mod2.rds                   # Saved Model 2
├── mod3.rds                   # Saved Model 3
└── README.md
```

---

## Requirements

### R Packages
```r
library(tidyverse)
library(haven)
library(readxl)
library(lme4)
library(broom.mixed)
library(modelsummary)
library(ggeffects)
library(ggrepel)
library(knitr)
library(kableExtra)
library(patchwork)
library(countrycode)
library(vdemdata)
```

### Data Access
- **Eurobarometer 493 (ZA7575)** — available from [GESIS](https://www.gesis.org)
- **V-Dem** — available via the `vdemdata` R package: `install_github("vdeminstitute/vdemdata")`

---

## Citation

Maerz, Seraphine F., Amanda B. Edgell, Sebastian Hellemeier, Nina Illchenko, and Linnea Fox. 2025. *vdemdata: An R package to load, explore and work with the most recent V-Dem dataset.* https://github.com/vdeminstitute/vdemdata
