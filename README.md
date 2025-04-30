## CAST: Time-Varying Treatment Effects with Application to Chemotherapy and Radiotherapy on Head and Neck Squamous Cell Carcinoma

## Overview

This repository contains the implementation of CAST, a framework designed to model time-varying treatment effects in survival analysis. Specifically, the framework is applied to chemotherapy and radiotherapy treatment outcomes for Head and Neck Squamous Cell Carcinoma (HNSCC). By estimating how treatment effects evolve over time, CAST aims to provide more accurate insights into the long-term impact of these treatments, supporting personalized treatment strategies in clinical oncology.

The repository includes:
- Data simulation functions to generate synthetic datasets with realistic treatment effects.
- Propensity score modeling using elastic net regression.
- Causal survival forests to estimate treatment effects, capturing heterogeneous impacts at multiple time points.
- Time-varying treatment effect estimation, leveraging both parametric and non-parametric methods.
- Robustness checks such as dummy outcome tests and refutation tests with fake confounders.
- Visualizations including treatment effect distributions, Kaplan-Meier survival curves, SHAP values, and more.

Additionally, the framework is demonstrated on a real-world dataset, **RADCURE**, a dataset containing clinical data for HNSCC patients treated with chemotherapy and/or radiotherapy. The real dataset allows for the application of CAST in a clinical context, providing practical insights into treatment effect heterogeneity over time.

## Code Structure

### 1. Data Simulation
The `simulate_simple_data()` function generates synthetic survival data with covariates like age, sex, and tumor site, and calculates survival times based on treatment effects. It simulates a dataset with treatment assignments and survival times, which can be saved as `simulated_data.csv`.

### 2. Propensity Score Estimation
The `fit_propensity_model()` function estimates propensity scores for treatment assignment using elastic net logistic regression. These scores are essential for controlling for confounding in the treatment effect estimation.

### 3. Causal Forest Estimation
The `implement_causal_forests()` function applies causal survival forests to estimate Average Treatment Effects (ATE) for survival probability (SP) and restricted mean survival time (RMST) at various time horizons (12, 24, 36, 48 months, etc.).

### 4. Time-Varying Treatment Effects
The `model_temporal_treatment_effects()` function models time-varying treatment effects using both parametric (quadratic) and non-parametric (smoothing splines) approaches. This helps capture treatment effect trajectories over time, which are crucial for understanding long-term outcomes of chemotherapy and radiotherapy.

### 5. Visualization
The code generates a series of plots to help visualize and interpret treatment effects:
- Treatment Effect Distributions: Histograms of individual treatment effects across different time points are generated using `plot_effects_distribution()`.
- Kaplan-Meier Survival Curves: Using `ggsurvplot()`, Kaplan-Meier plots display survival probabilities over time for treated and control groups.
- SHAP Value Explanations: The `fastshap::explain()` function generates SHAP values to understand the contribution of each feature to the treatment effect predictions. Plots show how features like Age, Sex, and HPV status influence survival probability (SP) and RMST estimates.
- Combined Parametric and Non-Parametric Model Plots: Comparison plots are generated to visualize both parametric (quadratic) and non-parametric (smoothing splines) models of treatment effects over time.

### 6. Robustness Checks
The repository includes tests to validate the robustness of the treatment effect estimates:
- Dummy Outcome Tests: These tests shuffle the outcome variable to simulate random noise, ensuring that the causal model doesn’t produce spurious results.
- Refutation Tests with Fake Confounders: These tests add fake confounders to check if the treatment effect estimates are sensitive to irrelevant variables.
- Negative Control Tests: For example, irrelevant causal variables (like randomly generated binary vectors) are tested to ensure they don’t impact the estimated treatment effects.

### 7. Propensity Score Modeling
The `fit_propensity_model()` function generates propensity scores using logistic regression with elastic net regularization, which are essential for controlling confounding in the causal forest model. Propensity scores are predicted and saved in the dataset, ensuring proper adjustment for confounding factors.

## RADCURE Dataset

**RADCURE** is a real-world clinical dataset that contains data on patients diagnosed with Head and Neck Squamous Cell Carcinoma (HNSCC), a cancer that arises from the mucosal lining of the upper aerodigestive tract. The dataset includes variables on patient demographics, tumor characteristics, and treatment information, such as whether the patients received chemotherapy, radiotherapy, or both.

RADCURE is used in this framework to demonstrate the applicability of the CAST method in a real-world setting. The data from RADCURE enables us to model time-varying treatment effects for chemotherapy and radiotherapy, capturing the heterogeneous effects of these treatments over time. The dataset's detailed treatment and survival information provide a foundation for testing the effectiveness of CAST in estimating the long-term outcomes for HNSCC patients.

The **RADCURE** dataset is pre-processed and used in conjunction with the synthetic data for validation and testing purposes. It allows us to perform a more robust analysis of the treatment effects over time, providing valuable insights into how these treatments influence survival and recovery outcomes for patients with HNSCC.

## Context and Motivation

This project focuses on modeling time-varying treatment effects in the context of Head and Neck Squamous Cell Carcinoma (HNSCC). Traditional methods estimate treatment effects at fixed time points (e.g., at the end of treatment), but these effects may evolve over time. The CAST framework allows us to model how treatment effects change over time, enabling more personalized treatment strategies.

In the case of HNSCC, understanding the temporal dynamics of chemotherapy and radiotherapy impacts is crucial for tailoring treatment plans. By capturing these time-varying effects, CAST offers a more comprehensive view of how therapies like chemotherapy and radiotherapy affect survival outcomes at different stages of the disease.

## Outputs

The following results are generated:
1. Treatment Effect Estimates: CSV files containing ATE for SP and RMST at multiple time horizons.
2. Visualizations: Plots for treatment effects, Kaplan-Meier curves, and SHAP-based explanations.
3. Robustness Test Results: Results from dummy outcome tests and refutation tests, saved as CSV files for validation.

#### To run the analysis, execute the script `Final_novel_R_propensity_EY.r`.

---

This repository is maintained anonymously, and the project is being submitted to a top-tier venue in machine learning for review.
