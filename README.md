# COVID-19 Restrictions and Air Quality in European Cities

DA4 Term Project — Central European University

## Research Question

Do stricter COVID-19 restrictions reduce urban air pollution? We use panel data on 120 cities across 9 European countries (2020--2022) to estimate the causal effect of the Oxford Stringency Index on NO2 concentrations using a two-way fixed effects framework.

## Folder Structure

```
da4_term_project/
├── README.md
├── LICENSE
├── code/
│   ├── 1_covid_data_clean.ipynb       # Download & clean COVID policy data
│   ├── 2_pollution_data_download.ipynb # Download raw air quality data from AQICN
│   ├── 3_data_cleaning.ipynb          # Merge, clean, descriptive statistics
│   └── 4_causal_analysis.ipynb        # FE regressions, event study, robustness
├── data/
│   ├── raw/                           # Raw downloaded data (not transformed)
│   │   ├── covid_level1.csv
│   │   └── aqicn_all_cities_raw.csv
│   └── clean/                         # Analysis-ready datasets
│       ├── city_country_mapping.csv
│       ├── covid_policy_national.csv
│       └── panel_city_day.csv
└── output/
    ├── figures/                        # All plots (event study, time series, etc.)
    └── tables/
```

## Notebooks

| # | Notebook | What it does |
|---|---------|-------------|
| 1 | `1_covid_data_clean.ipynb` | Downloads national COVID-19 policy data via the `covid19dh` package for 9 EU countries. Extracts stringency index, individual policy indicators, and case counts. Builds a 126-city mapping. |
| 2 | `2_pollution_data_download.ipynb` | Downloads 12 quarterly CSVs (2020Q1--2022Q4) from the AQICN COVID-19 data platform. Filters to target cities, saves raw long-format data. |
| 3 | `3_data_cleaning.ipynb` | Pivots pollution data to wide format, analyzes missingness, merges with COVID policy data on country x date, drops 6 low-coverage cities, engineers features (log transforms, lags, time variables), produces descriptive statistics and visualizations. |
| 4 | `4_causal_analysis.ipynb` | Estimates progressive FE specifications (pooled OLS through TWFE + weather + country trends), event study around first major lockdown, robustness checks (alternative outcomes, leave-Italy-out, log vs. levels), and country-level heterogeneity analysis. |

## Reproduction

**Requirements:** Python 3.9+, Jupyter Notebook

```bash
pip install pandas numpy matplotlib seaborn pyfixest covid19dh
```

**Steps:**

1. Run `1_covid_data_clean.ipynb` — downloads COVID data via `covid19dh` (requires internet)
2. Run `2_pollution_data_download.ipynb` — downloads AQICN data (requires internet; ~5 min)
3. Run `3_data_cleaning.ipynb` — merges and cleans; produces `panel_city_day.csv`
4. Run `4_causal_analysis.ipynb` — runs all regressions and generates figures

If `data/raw/` files already exist, notebooks 1--2 skip the download automatically.

## Data Sources

- **COVID-19 policy data**: [COVID-19 Data Hub](https://covid19datahub.io/) via the `covid19dh` Python package (Guidotti & Ardia, 2020)
- **Air quality data**: [AQICN COVID-19 Data Platform](https://aqicn.org/data-platform/covid19/) — daily city-level pollutant and weather measurements
