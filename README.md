CLINICAL FACTORS ASSOCIATED WITH SEPTIC SHOCK OR MORTALITY IN PEDIATRIC INVASIVE MENINGOCOCCAL DISEASE: A RETROSPECTIVE STUDY FROM TWO TERTIARY HOSPITALS IN CHILE, 2009-2025.

Overview
This repository contains a reproducible statistical analysis of factors associated with septic shock or death among pediatric patients with invasive meningococcal disease (IMD). The workflow was developed to address methodological concerns related to small-sample multivariable modeling, separation, variable selection, missing data, and model stability.
The repository uses only the simulated dataset "simulated_pediatric_IMD_data.csv". No real patient-level or confidential clinical data are included.


Objectives
The analysis aims to:
- Estimate factors associated with the composite outcome of septic shock or death;

- Document the effect of complete-case analysis on the effective sample size;

- Reproduce the original forward AIC and Firth logistic regression procedure;

- Distinguish admission variables from complications arising during hospitalization;

- Evaluate collinearity, clinical overlap, separation, and coefficient stability;

- Compare alternative parsimonious and bias-reduced models; and

- Assess the sensitivity of the findings using bootstrap resampling, leave-one-out analysis, ridge regularization, and multiple imputation.

This project is intended as an explanatory association analysis, not as the development or external validation of a clinical prediction model.


Files
- simulated_pediatric_IMD_data.csv: Simulated pediatric IMD dataset used to reproduce the workflow without disclosing confidential patient data.

- pediatric-imd-risk-analysis.Rmd: Complete analysis, including statistical methods, tables, figures, sensitivity analyses, and information on reproducibility.

The R Markdown analysis includes: data import, variable-name mapping, and binary recoding; outcome and data-quality verification. Transparent classification of candidate variables by clinical domain and timing; missing-data profiling and evaluation of the impact of `complete.cases()`; exploratory univariable Firth logistic regression; phi correlations, variance inflation factors, contingency tables, and separation diagnostics; reproduction of forward AIC selection and the original Firth model.

Firth regression sensitivity models using the full cohort and admission variables; mean bias-reduced logistic regression with brglm2; ridge-penalized logistic regression with glmnet; bootstrap assessment of variable-selection stability; leave-one-out assessment of coefficient stability; multiple imputation by chained equations for lactate; and descriptive ROC/AUC analysis and sensitivity analysis of the composite outcome.


Requirements
The analysis was designed for R and requires the following packages:
install.packages(c(
  "rmarkdown", "knitr", "readr", "dplyr", "tidyr", "purrr",
  "stringr", "tibble", "ggplot2", "scales", "MASS", "logistf",
  "brglm2", "detectseparation", "glmnet", "mice", "pROC"
))

From the R console
rmarkdown::render(
  input = "pediatric-imd-risk-analysis-english.Rmd",
  params = list(
    data_path = "simulated_pediatric_IMD_data.csv",
    B_boot = 300,
    m_imputations = 50
  )
)

The number of bootstrap samples and imputations can be changed through the parameters B_boot and m_imputations. Lower values may be used for a quick test run, whereas larger values are preferable for the final analysis.

Input Data
The analysis expects a CSV file containing the composite outcome and the clinical, demographic, microbiological, and hospitalization variables used in the R Markdown document.


