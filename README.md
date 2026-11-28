# Replication Package for: "Housing Costs, Labour Market Exclusion and the Redistributive Limits of Welfare States: Evidence from a 21–Year European Macro Panel"

## 1. Overview
This replication package contains the full suite of R scripts used for data construction, validation, econometric modeling, and robustness checks for the manuscript submitted to the *International Journal of Social Economics*. 

The package is designed to provide 100% methodological transparency, allowing reviewers and readers to perfectly trace the steps from raw microdata aggregation to the final empirical tables presented in the paper.

## 2. Data Availability & Confidentiality
Please note that the core dataset relies on the **European Union Statistics on Income and Living Conditions (EU-SILC)** microdata. Due to strict data protection regulations and non-disclosure agreements enforced by Eurostat, the **raw microdata files (D, H, R, P files) cannot be shared publicly**. 

However, to facilitate full reproducible research, we provide the custom, bottom-up data-aggregation R script used to generate the macroeconomic variables, alongside the final aggregated macro-panel dataset (`Thesis_Final_Panel_Dataset_Bulletproof.csv`). This allows researchers to independently run all econometric models and validation checks without needing access to the restricted microdata.

## 3. Software Requirements
The code was written and tested in **R**. To execute the scripts seamlessly, please ensure the following R packages are installed:
- Data Manipulation: `dplyr`, `tidyr`, `stringr`, `data.table`
- API & Validation: `eurostat`
- Econometrics: `plm`, `lmtest`, `sandwich`, `car`
- Output & Formatting: `stargazer`

## 4. File Manifest
The repository contains the following scripts, structured in logical order of execution:

### A. Data Construction & Validation
- **`EUSILC DATABASE ALL YEARS`**: The master script that processes the raw EU-SILC microdata. It applies necessary patches, standardises variables, and applies cross-sectional weights to construct the national macro-aggregates.
- **`VERIFICATION EUROSTAT`**: An automated validation script that queries the official Eurostat API to download official macro-aggregates and calculates the Mean Absolute Error (MAE) against our constructed dataset.

### B. Summary Statistics & Main Econometric Analysis
- **`TABLE 1 SUMMARY STATISTICS`**: Calculates and exports the summary statistics for the full unbalanced panel (Table 1).
- **`ECONOMETRIC MODEL`**: Contains the baseline one-way fixed effects models with 1-year lagged independent variables. It applies Arellano clustered standard errors and directly exports Table 2.

### C. Diagnostics & Robustness Checks (Requested during Peer Review)
- **`DISCOLL KRAAY STANDARD ERRORS`**: Estimates the robustness check models using Two-Way Fixed Effects (Country & Year FE), executes Pesaran CD diagnostic tests across one-way and two-way specifications, and exports Table A3 (`maxlag = 2`).
- **`DIAGNOSTICS ECONOMETRICS TESTS`**: Executes formal diagnostic tests for heteroskedasticity (Breusch–Pagan) and serial correlation (Breusch–Godfrey/Wooldridge) across both Gini and S80/S20 models.
- **`DIAGNOSTICS HAUSMAN VIFS`**: Executes the robust Hausman specification test (FE vs. RE) and calculates the Variance Inflation Factors (VIFs) to rule out multicollinearity.
- **`ROBUSTNESS FAILED GMM`**: Provided for methodological transparency. This script contains the initially attempted two-step System GMM dynamic panel model (including collapsed instrument matrices and restricted lag depths), which was ultimately abandoned due to severe instrument proliferation.

### D. Appendix Tables
- **`TABLE A1 CORRELATION MATRIX`**: Generates and exports the Pearson Correlation Matrix alongside the Variance Inflation Factors (VIFs) to confirm the absence of severe multicollinearity (Table A1).
- **`TABLE A2 DATA COVERAGE`**: Generates and exports the unbalanced panel coverage map and yearly observations ($T$) per country (Table A2).
- **`TABLE A4 DRISCOLL KRAAY SES`**: Estimates the bandwidth sensitivity analysis for the Two-Way Fixed Effects models using Driscoll–Kraay standard errors with alternative maximum lags (`maxlag = 1` and `maxlag = 3`) and exports Table A4.
- **`TABLE A5 EU-SILC VARIABLE CONSTRUCTION`**: Generates and exports the comprehensive variable-mapping reference table detailing measurement units, raw EU-SILC target variable codes, survey weights, and cross-wave harmonisation rules (Table A5).
- **`TABLE A6 VALIDATION AND ROBUSTNESS`**: Queries the official Eurostat Housing Cost Overburden series (`ilc_lvho07a`) via API, re-estimates the baseline fixed-effects models for comparison against our bottom-up micro-aggregated indicator, and exports Table A6.

## 5. Instructions for Use
1. Save all scripts and the `Thesis_Final_Panel_Dataset_Bulletproof.csv` file in the same local directory.
2. Set that directory as your Working Directory in R (`setwd("path/to/folder")`) or open the folder as an RStudio Project.
3. You can execute any script from sections B, C, and D directly, as they load the provided `.csv` dataset using relative paths.
4. All tables (Table 1, Table 2, and Tables A1–A6) will be automatically exported to your working directory as formatted `.doc` files.

## 6. Contact
For any questions regarding the code or the dataset, please contact the corresponding author.
