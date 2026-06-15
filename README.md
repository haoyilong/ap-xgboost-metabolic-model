# Explainable Metabolic-Clinical XGBoost Model for Mortality Prediction in Acute Pancreatitis

[![DOI](https://zenodo.org/badge/XXXXXX.svg)](https://doi.org/10.5281/zenodo.XXXXXX)

## Overview

This repository contains the complete analysis codebase for the manuscript:

> **"Development, Geographic Plausibility Check, and External Validation of an Explainable Metabolic-Clinical XGBoost Model for Mortality Prediction in Acute Pancreatitis: A Dual-Cohort Study with DM-Stratified Confounding Control"**

## Key Features

- **Nested Incremental Modeling**: Quantify the contribution of metabolic data beyond clinical scores (SOFA, BISAP)
- **HbA1c-Independent DM Classification**: 4-dimension pragmatic diabetes mellitus stratification for ICU settings
- **TRIPOD+AI Compliant**: Full adherence to Transparent Reporting of a multivariable prediction model for Individual Prognosis Or Diagnosis -- Artificial Intelligence Statement
- **Explainable AI**: 4-dimensional SHAP (SHapley Additive exPlanations) analysis with DM-stratified interpretation
- **External Validation**: Geographic plausibility check using eICU-CRD multicenter cohort
- **Fairness Assessment**: 2,000-iteration bootstrap subgroup hypothesis testing

## Repository Structure

```
.
├── README.md                          # This file
├── CITATION.cff                       # Citation metadata
├── LICENSE                            # MIT License
├── code/
│   ├── 01_data_extraction_mimic.sql   # MIMIC-IV cohort extraction
│   ├── 02_data_extraction_eicu.sql    # eICU-CRD cohort extraction
│   ├── 03_model_development.R         # XGBoost model + nested CV
│   ├── 04_incremental_modeling.R      # Nested incremental modeling
│   ├── 05_calibration_dca.R           # Calibration & DCA analysis
│   ├── 06_shap_explainability.R       # SHAP global + subgroup analysis
│   ├── 07_fairness_bootstrap.R        # Bootstrap subgroup fairness tests
│   ├── 08_sensitivity_analysis.R      # DM definition sensitivity analysis
│   └── 09_landmarking.R               # Dynamic landmarking analysis
├── data/
│   └── (user-provided; not included)  # MIMIC-IV & eICU-CRD access required
├── results/
│   ├── FigA2_Model_Comparison.png     # Model comparison ROC curves
│   ├── FigA3_Calibration.png          # Calibration plots
│   ├── FigA4_SHAP_Global.png          # Global SHAP feature importance
│   ├── FigA8_DCA_Overall.png          # Decision curve analysis
│   ├── FigA10_Landmarking.png         # Dynamic landmarking
│   ├── FigA11_Nomogram.png            # Clinical nomogram
│   ├── FigA12_Fairness.png            # Fairness assessment
│   ├── Fig_CONSORT_Flow.png           # CONSORT flow diagram
│   ├── Fig_Incremental_Model.png      # Incremental modeling results
│   └── Fig_Nomogram.png               # Simplified nomogram
└── tables/
    ├── Table1_Baseline_Characteristics.csv
    ├── Table2_Model_Performance.csv
    ├── Table3_Incremental_Modeling.csv
    ├── Table4_Subgroup_Analysis.csv
    ├── Table5_DCA_Thresholds.csv
    ├── Table6_Sensitivity_Analysis.csv
    ├── Table7_Method_Details.csv
    └── Table8_PROBAST_Assessment.csv
```

## Data Requirements

This study uses two publicly available critical care databases:

1. **MIMIC-IV v2.2** (development cohort): Requires credentialing via [PhysioNet](https://physionet.org/content/mimiciv/)
2. **eICU-CRD v2.0** (external validation): Requires credentialing via [PhysioNet](https://physionet.org/content/eicu-crd/)

Both databases are available through PhysioNet after completing the required training (CITI Program).

## Software Requirements

- R >= 4.2.0
- Python >= 3.9
- R packages: `xgboost`, `SHAPforxgboost`, `pROC`, `rms`, `mice`, `caret`, `dcurves`, `survival`, `glmnet`, `isotone`
- Python packages: `pandas`, `numpy`, `scikit-learn`, `matplotlib`, `seaborn`

## Usage

### 1. Data Extraction

```bash
# MIMIC-IV cohort (requires PostgreSQL with MIMIC-IV loaded)
psql -d mimiciv -f code/01_data_extraction_mimic.sql > data/mimic_cohort.csv

# eICU-CRD cohort
psql -d eicu -f code/02_data_extraction_eicu.sql > data/eicu_cohort.csv
```

### 2. Model Development & Validation

```r
# Run complete analysis pipeline
source("code/03_model_development.R")      # Main XGBoost model
source("code/04_incremental_modeling.R")   # Nested incremental modeling
source("code/05_calibration_dca.R")        # Calibration & DCA
source("code/06_shap_explainability.R")    # SHAP analysis
source("code/07_fairness_bootstrap.R")     # Bootstrap fairness tests
source("code/08_sensitivity_analysis.R")   # Sensitivity analyses
source("code/09_landmarking.R")            # Dynamic landmarking
```

## Key Results Summary

| Metric | Value |
|--------|-------|
| MIMIC-IV CV-AUC | 0.851 (95% CI: 0.822-0.877) |
| eICU-CRD External AUC | 0.815 (95% CI: 0.730-0.890) |
| Brier Score | 0.080 |
| Calibration Slope | 1.000 |
| Metabolic Panel ΔAUC vs SOFA | +0.080 |
| NRI (vs SOFA) | 0.704 |
| IDI (vs SOFA) | 0.136 |

## Citation

If you use this code or data, please cite:

```
[First Author], [Second Author], [Third Author]. Development, Geographic Plausibility 
Check, and External Validation of an Explainable Metabolic-Clinical XGBoost Model for 
Mortality Prediction in Acute Pancreatitis: A Dual-Cohort Study with DM-Stratified 
Confounding Control. BMC Medical Informatics and Decision Making. 2026.
```

## License

This project is licensed under the MIT License - see [LICENSE](LICENSE) file.

The analysis code is open source. The underlying clinical data (MIMIC-IV, eICU-CRD) are 
governed by their respective PhysioNet data use agreements.

## Contact

Corresponding author: [email@institution.edu]

For code-related questions, please open an issue on this repository.

## Acknowledgments

- MIMIC-IV and eICU-CRD are maintained by the MIT Laboratory for Computational Physiology 
  and the Philips eICU Research Institute
- This study was conducted in accordance with the TRIPOD+AI Statement (2024) and PROBAST guidelines
