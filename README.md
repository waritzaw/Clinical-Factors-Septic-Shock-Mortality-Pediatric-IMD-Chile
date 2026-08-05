Pediatric Invasive Meningococcal Disease Risk Analysis



Overview

This repository contains a reproducible statistical reanalysis of factors associated with septic shock or death among pediatric patients with invasive meningococcal disease (IMD). The workflow was developed to address methodological concerns related to small-sample multivariable modeling, separation, variable selection, missing data, and model stability.

The repository uses only the simulated dataset simulated_pediatric_IMD_data.csv. No real patient-level or confidential clinical data are included.

Objectives

The analysis aims to:

estimate factors associated with the composite outcome of septic shock or death;

document the effect of complete-case analysis on the effective sample size;

reproduce the original forward AIC and Firth logistic regression procedure;

distinguish admission variables from complications arising during hospitalization;

evaluate collinearity, clinical overlap, separation, and coefficient stability;

compare alternative parsimonious and bias-reduced models; and

assess the sensitivity of the findings using bootstrap resampling, leave-one-out analysis, ridge regularization, and multiple imputation.

This project is intended as an explanatory association analysis, not as the development or external validation of a clinical prediction model.

Repository Structure

.
├── README.md
├── pediatric-imd-risk-analysis-english.Rmd
├── simulated_pediatric_IMD_data.csv
└── reviewer3_comment4_results/          # Created automatically when the analysis is run

Main files

File

Description

pediatric-imd-risk-analysis-english.Rmd

Complete analysis written in English, including statistical methods, tables, figures, sensitivity analyses, and reproducibility information.

simulated_pediatric_IMD_data.csv

Simulated pediatric IMD dataset used to reproduce the workflow without disclosing confidential patient data.

reviewer3_comment4_results/

Automatically generated directory containing figures, result tables, package versions, and session information.

Statistical Workflow

The R Markdown analysis includes:

data import, variable-name mapping, and binary recoding;

outcome and data-quality verification;

transparent classification of candidate variables by clinical domain and timing;

missing-data profiling and evaluation of the impact of complete.cases();

exploratory univariable Firth logistic regression;

phi correlations, variance inflation factors, contingency tables, and separation diagnostics;

reproduction of forward AIC selection and the original Firth model;

Firth regression sensitivity models using the full cohort and admission variables;

mean bias-reduced logistic regression with brglm2;

ridge-penalized logistic regression with glmnet;

bootstrap assessment of variable-selection stability;

leave-one-out assessment of coefficient stability;

multiple imputation by chained equations for lactate; and

descriptive ROC/AUC analysis and sensitivity analysis of the composite outcome.

Requirements

The analysis was designed for R and requires the following packages:

install.packages(c(
  "rmarkdown", "knitr", "readr", "dplyr", "tidyr", "purrr",
  "stringr", "tibble", "ggplot2", "scales", "MASS", "logistf",
  "brglm2", "detectseparation", "glmnet", "mice", "pROC"
))

Exact package versions used during execution are written to:

reviewer3_comment4_results/software_versions.csv
reviewer3_comment4_results/sessionInfo.txt

How to Run the Analysis

From RStudio

Clone or download this repository.

Open pediatric-imd-risk-analysis-english.Rmd in RStudio.

Confirm that simulated_pediatric_IMD_data.csv is in the same directory.

Select Knit to generate the HTML or Word report.

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

The import routine supports the original Spanish column names and maps them to English aliases used internally. Binary variables may be represented as:

0 and 1;

Yes and No;

Y and N; or

Sí and No.

The main outcome is internally named adverse_outcome and corresponds to septic shock or death.

Generated Outputs

Running the analysis creates the directory reviewer3_comment4_results/, which may include:

missing-data and correlation plots;

comparative forest plots;

bootstrap selection-frequency results;

leave-one-out coefficient-stability plots;

univariable and multivariable model tables;

ridge-regression coefficients;

multiple-imputation results;

software-version records; and

complete R session information.

Interpretation Notes

Firth logistic regression reduces small-sample bias and produces finite estimates under separation, but it does not eliminate overfitting or uncertainty arising from data-driven variable selection. For this reason, the analysis prioritizes parsimonious models and reports several sensitivity and stability assessments.

Variables recorded during hospitalization, such as multiorgan failure, should not automatically be interpreted as baseline prognostic factors. Results should be described as exploratory associations within the analyzed cohort.

Data Privacy and Ethical Use

The original clinical data underlying the research are confidential and are not distributed through this repository. The public dataset is entirely simulated and is provided only for reproducibility, teaching, code testing, and methodological demonstration.

The simulated data must not be interpreted as real clinical observations or used to make patient-level decisions.

Reproducibility

A fixed random seed is used in the analysis:

set.seed(20260802)

Nevertheless, results may vary slightly across R or package versions, particularly for cross-validation, multiple imputation, and iterative estimation procedures. The generated software-version files should be retained with archived results.

References

The methodological framework is based on literature concerning Firth logistic regression, sparse-data bias, variable selection, multiple imputation, regularization, and internal stability assessment. Complete references are provided in Section 20 of the R Markdown report.

Citation

When reusing or adapting this workflow, please cite the repository and the corresponding scientific publication, once available.

Suggested repository citation:

Research Team. Pediatric Invasive Meningococcal Disease Risk Analysis:
A reproducible small-sample logistic regression workflow using simulated data.
GitHub repository, 2026.

License

Add the license selected for the repository in a separate LICENSE file. The code and simulated data should be licensed separately when their permitted uses differ.
