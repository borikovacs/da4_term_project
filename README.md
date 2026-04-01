# DA4 Term Project: Air Quality and Environmental Policy in European Cities

## Research Question

**Does the introduction of low-emission zones (LEZs) or diesel bans in European cities reduce air pollution?**

## Summary

We use city-level air quality panel data from the [Air Quality API](https://aqicn.org/api/) (or OpenAQ) combined with policy intervention data to estimate the causal effect of environmental regulations on air pollution outcomes. The treatment is the adoption of a **Low Emission Zone (LEZ)** — a geographically defined area where vehicle access is restricted based on emission standards (e.g., diesel bans, Euro-norm requirements).

## Treatment: Low Emission Zones (LEZs)

- LEZs have been rolled out **at different times** across European cities — this staggered adoption is key for identification
- Data on LEZ adoption dates and scope is available from [Urban Access Regulations](https://urbanaccessregulations.eu/) and Eurostat
- Recommended measure: **binary indicator** for whether a city has an active LEZ in a given period (month/quarter)

## Identification Strategy

- **Difference-in-Differences (DiD)** or **Event Study** exploiting staggered LEZ rollout across cities
- Treated group: cities that adopt LEZs; Control group: cities that have not (yet) adopted
- Event study to visualize pre-trends and dynamic treatment effects

## Key Considerations

- **Parallel trends**: check with event-study plot; pre-treatment trends should be flat
- **Differential trends**: cities adopting LEZs may already be on different pollution trajectories — control for:
  - Urbanisation level (population density, urban/rural classification)
  - Economic activity (GDP per capita, from Eurostat)
  - Weather/seasonality (temperature, wind — from weather APIs)
  - Traffic volume if available
- **Spillover effects**: LEZs in one city may divert traffic to neighboring cities — could test for this as an extension
- **Heterogeneity**: effects may differ by city size, strictness of the LEZ, baseline pollution level

## Data

| Variable | Source | Role |
|---|---|---|
| Air quality (PM2.5, PM10, NO2) | Air Quality API / OpenAQ | **Outcome (Y)** |
| LEZ adoption (date, scope) | Urban Access Regulations / Eurostat | **Treatment (X)** |
| Population / urbanisation | Eurostat | Control |
| GDP per capita (regional) | Eurostat | Control |
| Weather (temp, wind) | Weather API | Control |

- **Panel structure**: city × month (or quarter)
- Target: N ≥ 100 cities, T ≥ 12 periods (monthly data over several years)

## Robustness & Extensions

- Alternative pollution measures (PM2.5 vs NO2)
- Varying treatment definition (strictness levels of LEZ)
- Placebo tests with fake adoption dates
- Spillover analysis on neighboring non-LEZ cities
- Heterogeneity by city size or baseline pollution

## Project Structure

```
da4_term_project/
├── README.md
├── code/
│   ├── 01_data_cleaning.ipynb
│   └── 02_analysis.ipynb
├── data/
│   ├── raw/
│   └── clean/
└── output/
    ├── figures/
    └── tables/
```
