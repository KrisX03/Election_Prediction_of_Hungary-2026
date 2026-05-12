# Forecasting the 2026 Hungarian Parliamentary Election

This repository accompanies my TDK research project at Corvinus University of Budapest. I forecast the 2026 Hungarian parliamentary election by combining polls, socio-economic fundamentals, online media consumption signals and Monte Carlo seat simulations. The repository contains the paper, the presentation materials, the data, the notebooks, the figures and the forecast outputs.

## Recognition

- **1st place** at TDK in the Network and Data Science session, awarded for the paper together with the oral presentation.
- **Nominated for OTDK** (Országos Tudományos Diákköri Konferencia, the national student research competition).
- **Nominated for Best Paper.**

## Author

Kristóf Andrási

## Motivation

I chose the 2026 Hungarian parliamentary election as the case study because it has now taken place. This allowed me to not only build a forecast but also evaluate it against the realised outcome. I also pre-registered the predictions before election day, so the exercise stands as a genuine out-of-sample test. The research question is straightforward. How can we combine information from polls and other sources to produce a good election forecast?

## Project overview

The analysis covers the last two Hungarian parliamentary elections and the last two European Parliament elections for training and validation. It then delivers a pre-election forecast for the 2026 vote.

- 2018 Hungarian parliamentary election
- 2019 European Parliament election
- 2022 Hungarian parliamentary election
- 2024 European Parliament election
- 2026 Hungarian parliamentary election forecast and post-election evaluation

I work with political blocs rather than individual party labels, since the Hungarian party system has shifted across cycles. For 2026 the main bloc labels are government, opposition/TISZA, radical opposition/Mi Hazánk and other parties.

For the full method, results and discussion I refer the reader to the paper and the presentation in `doc/`.

## Data sources

The analysis draws on three main data domains.

- **Election results and polls** come from Prof. Gábor Tóka, who has been collecting Hungarian polls since 2014. Stored under `data/TokaGabor/`.
- **Socio-economic fundamentals** come from KSH and cover population, demographic structure, income, employment, CPI-related indicators and settlement-level statistics. Stored under `data/KSH/`.
- **Online media usage** comes from Gemius and covers outlets such as Telex, Index, 24.hu, RTL and TV2. To classify outlets as government-aligned or opposition-aligned I rely on ÁTLÁTSZÓ.HU's data on government financing of the press.

## Important notes

- **Raw Gemius data is not included.** Due to licensing restrictions `data/Gemius/` is empty in this upload. `03_media_usage.ipynb` and the media-related parts of `13_final_2026_forecast.ipynb` require those files to run end to end.
- **Generated data is not included.** `data/created/` is empty and is populated when `01_data_preparation.ipynb` is run.
- **Some paths may need adjustment.** I developed the notebooks locally, so some cells may contain absolute or workspace-specific paths.
- **The transcript is AI-generated.** `doc/presentation_transcript_AI.pdf` is an AI transcript of my oral TDK presentation and is included as supporting documentation.

## Method overview

From the polls and from the demographic fundamentals I derive a national list share prediction. From the district lean model I obtain district level list shares. From the candidate gap model I obtain individual candidate vote shares. I then translate these vote predictions into seats under Hungary's mixed electoral system (106 single member district seats and 93 national list seats allocated by the D'Hondt rule) and quantify uncertainty with 1,500 Monte Carlo draws. All tuning and model selection was validated through Leave-One-Election-Out (LOEO) cross-validation. The paper in `doc/` provides the full specification.

## Repository structure

```text
.
├── data/
│   ├── created/                    # Generated cleaned datasets. Empty until notebooks are run.
│   ├── Gemius/                     # Empty. Raw Gemius data cannot be redistributed.
│   ├── KSH/                        # Socio-economic and settlement-level data
│   └── TokaGabor/                  # Polls and historical election results
├── doc/
│   ├── Election_Forecast_Kristof_Andrasi.pdf
│   ├── Pre-Election Forecast Kristof Andrasi.pdf
│   ├── FINAL_TDK_Corvinus_PPT_2026.pdf
│   └── presentation_transcript_AI.pdf
├── final_final_scripts/
│   ├── 01_data_preparation.ipynb
│   ├── 02_exploratory_analysis.ipynb
│   ├── 03_media_usage.ipynb
│   ├── 12_fixed_params_LOEO.ipynb
│   ├── 13_final_2026_forecast.ipynb
│   ├── 13_final_2026_forecast_export.json
│   └── 14_final_results.ipynb
├── graphs_tables/                  # Generated figures and LaTeX tables
└── README.md
```

## Main notebooks

- `01_data_preparation.ipynb`. Cleans, harmonises and merges the source data.
- `02_exploratory_analysis.ipynb`. Explores historical election patterns and socio-economic correlations.
- `03_media_usage.ipynb`. Builds media usage indicators from Gemius data.
- `12_fixed_params_LOEO.ipynb`. Runs Leave-One-Election-Out validation with fixed parameters.
- `13_final_2026_forecast.ipynb`. Main pre-election forecasting notebook.
- `14_final_results.ipynb`. Post-election comparison and accuracy evaluation.

## Outputs

- Forecast export. `final_final_scripts/13_final_2026_forecast_export.json`
- Figures and tables. `graphs_tables/`
- Paper and presentation PDFs. `doc/`

## License

No license file is included in this upload. Before reusing or redistributing the code or data, please add an explicit license and respect the licensing terms of the original data providers.
