AP-XGBoost-Metabolic-Model

Development and External Validation of an Explainable Metabolic-Clinical XGBoost Model for Mortality Prediction in Acute Pancreatitis: A Dual-Cohort Study with DM-Stratified Confounding Control
Overview

This repository contains the complete analysis codebase for the TRIPOD+AI compliant acute pancreatitis (AP) mortality prediction model, developed on MIMIC-IV v3.1 and externally validated on eICU-CRD v2.0.
Citation

If you use this code, please cite:
plain

Hao Y, et al. Development and External Validation of an Explainable Metabolic-Clinical 
XGBoost Model for Mortality Prediction in Acute Pancreatitis: A Dual-Cohort Study with 
DM-Stratified Confounding Control. [Journal Name]. [Year].
DOI: 10.5281/zenodo.XXXXXXX
Repository Structure

plain

.
├── README.md                 # This file
├── CITATION.cff              # Citation metadata
├── LICENSE                   # MIT License
├── code/
│   ├── sql/                  # SQL extraction scripts (MIMIC-IV v3.1 + eICU-CRD v2.0)
│   ├── python/               # Python preprocessing & modeling pipeline
│   └── r/                    # R statistical verification scripts
Requirements

Python 3.12 (scikit-learn 1.5, XGBoost 2.0, SHAP 0.44)
PostgreSQL 14+ (for MIMIC-IV/eICU-CRD)
R 4.3+ (for statistical verification)
Data Sources

MIMIC-IV v3.1: https://physionet.org/content/mimiciv/3.1/
eICU-CRD v2.0: https://physionet.org/content/eicu-crd/2.0/
Both databases require PhysioNet credentialing and CITI training.
Key Features

Nested incremental modeling: Quantifies metabolic panel contribution beyond SOFA/BISAP
4-dimension DM classification: HbA1c-independent DM stratification for ICU settings
Isotonic calibration: Optimizes probability calibration while preserving discrimination
4D SHAP analysis: Global, individual, subgroup, and interaction explainability
Bootstrap fairness: 2,000-iteration subgroup hypothesis testing
Dynamic landmarking: AUC trajectory at Days 1, 2, 3, 5, 7, 14
License

MIT License — see LICENSE file.
Contact

Hao Yilong — Pudong New Area People's Hospital, Shanghai Jiao Tong University School of Medicine
