# Hungarian Election Predictions – Socio-Economic and Polling Analysis
## Predictive modeling of parliamentary and EP elections

This project was written for the TDK (Tudományos Diákköri Konferencia / Scientific Students' Associations Conference) at Corvinus University of Budapest.

### Author
- Kristóf Andrási  


---

## Project overview

This repository contains the data, analysis scripts, and modeling for a comprehensive study on **Hungarian election outcomes**, with a focus on forecasting the 2026 Hungarian parliamentary election (election day: 12 April 2026). The project predicts results at both the national and individual constituency (OEVK) levels by integrating three distinct data domains:

1.  **Historical Election Results:** Detailed outcomes from 2018, 2019 (EP), 2022, and 2024 (EP).
2.  **Socio-Economic Indicators:** Demographic, income, and employment data from the Hungarian Central Statistical Office (KSH).
3.  **Online Audience Data:** Digital consumption patterns and reach statistics from Gemius Audience.

The objective is to identify which socio-economic factors (e.g. education, income, urbanization) and digital footprints most strongly correlate with party preferences and to build a predictive model for future electoral cycles.

---

## Important notes for users

-   **Gemius data not included.** Due to licensing restrictions the raw Gemius Audience files cannot be redistributed. The `data/Gemius/` folder is therefore empty in this upload. Notebooks that use Gemius data (notably `03_media_usage.ipynb` and the media-related parts of `13_final_2026_forecast.ipynb`) will not run end-to-end without supplying this source separately.
-   **File paths may need to be adjusted.** The notebooks were written on a local machine and contain absolute or workspace-specific paths in some cells. Before running any notebook, check the file path variables at the top of the notebook and adapt them to your own directory layout.
-   **`data/created/` is empty.** This folder is the output target for cleaned and merged datasets produced by `01_data_preparation.ipynb`. It will be populated automatically the first time you run that notebook.

---

## Data

The project uses a multi-layered dataset compiled from several primary sources:

-   **Tóka Gábor / Vox Populi:** Historical election results (2018–2024) at the settlement, OEVK, and polling station levels, including pre-election polls. Located in `data/TokaGabor/`.
-   **KSH (Központi Statisztikai Hivatal):** Located in `data/KSH/`.
    -   Population counts by district (járás) and constituency.
    -   Socio-economic indicators: CPI (via World Bank mirror), employment rates, education levels and per capita income.
    -   Settlement-level statistical yearbooks (2016–2024).
-   **Gemius Audience:** Online audience reach and demographic data for Hungary (2022–2024), used as a proxy for regional interest and digital engagement. Not included in this repository (see notes above).
-   **Processed data:** Cleaned versions of the above are generated into `data/created/` by the data preparation notebook.

---

## Methods

The analytical pipeline follows a standard data science lifecycle:

### 1. Data Preparation & Integration
-   Merging different Excel and RData files into a unified daily and yearly panel.
-   Mapping KSH settlement-level statistics to the 106 Individual Electoral Constituencies (OEVK).
-   Cleaning and normalising polling data from various agencies to make them comparable.

### 2. Exploratory Analysis
-   Distribution analysis of voting patterns across the 106 constituencies.
-   Correlation mapping between KSH socio-economic variables and party performance.
-   Comparison with international forecasting methodologies (The Economist, Harvard, Zurich Uni) used to benchmark the approach.

### 3. Predictive Modeling
-   A 5-layer pipeline combining a national poll model, a structural fundamentals prior (Ridge regression on district demographics), a poll-plus-fundamentals combination, a district lean model, and a seat simulation step (block-level compensation vote approximation plus D'Hondt, 1500 Monte Carlo draws).
-   Two parallel paths for the national poll layer: a sample-weighted 60-day average and a house-effects plus Kalman random-walk filter.
-   Validation against historical 2018, 2019, 2022 and 2024 results to test model accuracy.

---

## Repository structure

```text
.
├── data/
│   ├── created/                    # Cleaned & merged datasets (populated by 01_data_preparation.ipynb)
│   ├── KSH/                        # Socio-economic data (population, income, CPI, employment)
│   │   ├── cpi_worldbank/
│   │   ├── telepules_szintu/       # Settlement-level yearbooks (2016–2024)
│   │   └── teruleti_munkval_jov/
│   ├── TokaGabor/
│   │   ├── Nyers_adatok/           # Raw poll database and documentation
│   │   └── Választási_eredmények/  # Historical election results (2018–2024)
│   └── Gemius/                     # Empty – source files cannot be redistributed
├── final_final_scripts/
│   ├── 01_data_preparation.ipynb       # Cleaning, merging and KSH-to-OEVK mapping
│   ├── 02_exploratory_analysis.ipynb   # Visualisations and descriptive statistics
│   ├── 03_media_usage.ipynb            # Gemius-based media reach analysis (needs Gemius data)
│   ├── 12_fixed_params_LOEO.ipynb      # LOEO validation with fixed parameters
│   ├── 13_final_2026_forecast.ipynb    # Full pipeline, main forecasting notebook
│   ├── 13_final_2026_forecast_export.json  # Exported 2026 forecast numbers
│   ├── 14_final_results.ipynb          # Post-election comparison and accuracy
│   └── palette_variations_preview.html # Colour palette preview for figures
├── graphs_tables/                  # Output figures (.png) and LaTeX tables (.tex)
├── doc/                            # Written outputs and slide decks (PDF)
│   ├── Election_Forecast_Kristof_Andrasi.pdf
│   ├── Pre-Election Forecast Kristof Andrasi.pdf
│   ├── FINAL_TDK_Corvinus_PPT_2026.pdf
│   └── presentation_transcript_AI.pdf
└── README.md
```

### Licence
MIT License (MIT): see the [License File](https://github.com/sensiolabs/GotenbergBundle/blob/1.x/LICENSE) for more details.
