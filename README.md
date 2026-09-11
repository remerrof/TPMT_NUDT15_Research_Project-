# Pharmacogenomic Profiling & Machine Learning for MRD Risk Prediction in Paediatric ALL

This repository contains the analysis pipelines, machine learning models, and evaluation scripts for the MSc thesis **"Pharmacogenomic Profiling and Modelling of *TPMT* and *NUDT15* Expression for Measurable Residual Disease Prediction in Paediatric Acute Lymphoblastic Leukaemia"** (University College Dublin, 2026).

---

## 📌 Project Overview

Measurable Residual Disease (MRD) following induction therapy is one of the strongest prognostic factors in paediatric Acute Lymphoblastic Leukaemia (ALL). This project investigates:
1. Whether gene expression levels of thiopurine metabolic enzymes—specifically ***TPMT*** and ***NUDT15***—are associated with post-induction MRD status.
2. Whether transcriptomic profiles (targeted gene panels vs. genome-wide expression) can train Machine Learning classifiers to predict end-of-induction MRD-positivity.
3. The relationship between inherited germline star-alleles (*TPMT* and *NUDT15* loss-of-function variants), gene expression levels, and clinical outcomes.

---

## 📊 Summary of Findings

* **Gene Expression & MRD:** *TPMT* transcript levels were significantly elevated in MRD-positive patients within the primary cohort (TARGET-ALL-P2, $n=433, p = 0.0001$). However, this association did not replicate in the independent validation cohort (MAGIC-I). *NUDT15* expression was not significantly associated with MRD status in either cohort.
* **Shared Transcriptional Signature:** Despite *TPMT* non-replication, a core set of 7 differentially expressed genes (including *NPR3*, *BIRC7*, *DSC3*, *GPR176*, and *NCKAP5*) showed significant cross-cohort overlap ($p = 0.011$).
* **Machine Learning Classifiers:**
  * Genome-wide Elastic Net models outperformed small targeted gene panels internally (TARGET-ALL-P2 ROC-AUC = 0.740 vs. 0.623).
  * All classifiers suffered performance loss when transferred to the smaller external validation cohort (MAGIC-I), highlighting challenges in cross-cohort generalisability due to biological heterogeneity.
* **Germline & eQTL Analysis:** Carriers of the loss-of-function ***TPMT\*3A*** allele displayed significantly lower *TPMT* transcript expression ($p = 0.025$). Cis-eQTL mapping indicated that *TPMT* expression in leukemic cells is driven primarily by disease subtype biology rather than inherited regulatory variants.

---

## 📁 Cohorts Studied

| Cohort | Sample Size ($n$) | Primary Data Types | Function in Study |
| :--- | :--- | :--- | :--- |
| **TARGET-ALL-P2**| 433 | RNA-seq, MRD Status, Subtypes| Discovery cohort, Differential Expression, Model Training|
| **MAGIC-I**| 43–70 | RNA-seq, WGS/WES, MRD Status| External Model Validation, Replication, Cis-eQTL Analysis|
| **EGA Datasets** | 46 | Germline WGS/WES, RNA-seq (subset)| Star-allele calling validation, Subtype associations|

---

## 🛠 Repository Structure

```text
.
├── data/
│   ├── metadata/            # Clinical & MRD metadata tables
│   └── process_expression/   # Normalised & batch-corrected RNA-seq matrices
├── scripts/
│   ├── 01_deg_analysis.R    # Differential gene expression & cross-cohort overlap
│   ├── 02_star_calling.py   # PyPGx star-allele calling pipeline (*TPMT* & *NUDT15*)
│   ├── 03_ml_classifiers.R # Machine learning model training (Elastic Net, RF, Logistic)
│   ├── 04_external_val.R    # External validation & calibration analysis on MAGIC-I
│   └── 05_eqtl_analysis.R   # Cis-eQTL scanning and variant annotations
├── models/                  # Saved model objects (.rds / .pkl)
├── figures/                 # ROC curves, Volcano plots, & Expression boxplots
└── README.md
