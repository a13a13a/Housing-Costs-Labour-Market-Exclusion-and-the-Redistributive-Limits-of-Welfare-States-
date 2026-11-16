# Replication Package: Housing Costs, Labour Market Exclusion and the Redistributive Limits of Welfare States

This repository contains the data and R code required to replicate the findings, tables, and econometric models presented in the manuscript: *"Housing Costs, Labour Market Exclusion and the Redistributive Limits of Welfare States: Evidence from a 21–Year European Macro Panel"* (International Journal of Social Economics).

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.XXXXXXX.svg)](https://doi.org/10.5281/zenodo.XXXXXXX) 
*(Note: Replace the badge above with your actual Zenodo DOI once you archive the repository).*

## 1. Data Availability Statement
The raw microdata used to construct the panel (European Union Statistics on Income and Living Conditions - EU-SILC) are confidential and subject to strict access and non-disclosure agreements enforced by Eurostat. Consequently, the raw micro-files cannot be shared publicly in this repository. 

However, to fully support reproducible research, this repository provides:
1. The **final aggregated macro-panel dataset** (`Thesis_Final_Panel_Dataset_Bulletproof.csv`) containing all variables used in the econometric estimations (N=32 countries, T=21 years).
2. The **Master Aggregation Script**, ensuring full methodological transparency regarding how raw EU-SILC microdata were cleaned, filtered, and aggregated into the final macroeconomic variables.

## 2. Repository Structure & Scripts

### 📁 Data
* `Thesis_Final_Panel_Dataset_Bulletproof.csv`: The final unbalanced macro-panel dataset (2004–2024).

### 📁 Scripts
* **`Master_Script_Bulletproof.R`**: The core data-aggregation pipeline. Extracts, harmonises, and aggregates raw EU-SILC microdata (files D, H, R, P) into national indicators, computing survey-weighted Gini, S80/S20, housing cost overburden, and labour market metrics.
* **`Eurostat_API_Validation.R`**: Benchmarks the custom-aggregated variables against official published Eurostat macroeconomic aggregates via the Eurostat API, calculating the Mean Absolute Error (MAE) for core indicators.
* **`Main_Econometric_Models.R`**: Contains the code to replicate the baseline country fixed-effects models (Table 2) and the two-way fixed-effects robustness checks with Driscoll-Kraay standard errors (Table A3).
* **`TableA1_CorrelationMatrix_VIF.R`**: Generates Table A1, computing the Pearson correlation matrix and the Variance Inflation Factors (VIFs) to test for multicollinearity.
* **`TableA2_DataCoverage.R`**: Generates Table A2, documenting the available time period and total country-year observations to explain the unbalanced panel structure.
* **`TableA4_Sensitivity_DK_Lags.R`**: Generates Table A4, conducting the sensitivity analysis for the two-way fixed effects models using alternative Driscoll-Kraay lag bandwidths (`maxlag = 1` and `maxlag = 3`).
* **`TableA5_Variable_Mapping.R`**: Generates Table A5, detailing the exact EU-SILC target variables, survey weights, and cross-wave harmonisation rules used for each constructed indicator.
* **`System_GMM_Attempt.R`**: Contains the initial two-step System GMM models. Included for full transparency to document the instrument proliferation issue (>270 instruments, singular covariance matrices, uninformative Sargan tests) that justified the adoption of the parsimonious Fixed Effects specification, as discussed in the manuscript's Limitations section.

## 3. How to Run the Code
1. Clone or download this repository to your local machine.
2. Ensure that the `Thesis_Final_Panel_Dataset_Bulletproof.csv` file is in your working directory.
3. If running the `Master_Script_Bulletproof.R`, note that you will need to map the `base_path` to your own locally stored EU-SILC UDB `.csv` files.
4. For all other scripts (Tables and Models), simply source the script in R. They are fully self-contained and will automatically read the provided `.csv` panel dataset and output the respective `.doc` tables or console summaries.

## 4. Software Dependencies
The code was written and tested in **R**. The following R packages are required:
* Data manipulation & API: `dplyr`, `tidyr`, `stringr`, `data.table`, `eurostat`
* Econometrics & Panel Data: `plm`, `car`, `lmtest`, `sandwich`
* Output & Formatting: `stargazer`

*Note: The `plm::vcovSCC()` function is used for the Driscoll-Kraay robust standard errors (Millo, 2017).*
