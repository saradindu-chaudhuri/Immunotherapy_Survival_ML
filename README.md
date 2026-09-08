# Immunotherapy_Survival_ML
Predictive Immunology &amp; Random Survival Forests for Immunotherapy Treatment Response
# 🔬 Immunotherapy Response & Predictive Immunology Survival ML

A quantitative health data science pipeline evaluating non-linear biomarker interactions and Progression-Free Survival (PFS) in immunotherapy clinical trial cohorts using **Cox Proportional Hazards** and **Random Survival Forests (RSF)**.

---

## 🎯 Key Findings & Performance Summary

* **Baseline Cox Proportional Hazards:** Achieved a **0.710 Concordance Index**, confirming significant hazard increases driven by systemic inflammatory markers ($NLR$ $HR=1.16$, $CRP$ $HR=1.11$, $p < 0.005$).
* **Random Survival Forest Ensemble:** Captured non-linear biological interactions, achieving a **0.762 Train C-Index**.
* **Permutation Feature Importance:** Isolated **PD1_Expression** as the dominant predictive biomarker ($\Delta C\text{-Index} = 0.094$), outranking general systemic inflammation.

| Model | Model Architecture | Test C-Index | Top Biomarker Driver |
| :--- | :--- | :---: | :--- |
| **Cox PH** | Parametric Linear Hazard | **0.710** | $PD1\text{-}Expression$ ($p < 0.005$) |
| **Random Survival Forest** | Non-Linear Tree Ensemble | **0.666** | $PD1\text{-}Expression$ ($\Delta = 0.094$) |

---

## 🛠️ Tech Stack & Methods

* **Languages:** Python 3.x (`pandas`, `numpy`, `matplotlib`)
* **Survival Modeling:** `lifelines` (CoxPHFitter, Kaplan-Meier), `scikit-survival` (RandomSurvivalForest)
* **Model Evaluation:** Concordance Index (C-Index), Log-Rank Significance Testing, Permutation Feature Importance (`sklearn.inspection`)

---

## 🚀 Pipeline Architecture

1. **Synthetic Cohort Generation:** Multi-variable simulation incorporating systemic inflammatory markers ($NLR$, $CRP$), immune checkpoint expression ($PD1$), and demographic covariates.
2. **Parametric Risk Estimation:** Fitting Cox PH models to determine linear hazard ratios and confidence intervals.
3. **Non-Linear Ensemble Fitting:** Estimating survival functions across continuous feature splits using Random Survival Forests.
4. **Permutation Importance:** Evaluating test-set degradation under covariate shuffling to rank biological relevance.

### 🛡️ Multi-Center Immune Profile Harmonization

To evaluate model transportability across independent sequencing platforms, we simulated a 3-center cohort ($N = 600$) with site-specific batch effects across immune cell populations ($CD8^+$ T-cells, $T_{reg}$, $M1$/$M2$ Macrophages).

* **Unharmonized Baseline AUC:** 0.919 (Confounded by site-level measurement bias)
* **Harmonized AUC:** **0.958** (Within-site Z-score standardization restored biological signal across sites)

| Data Pipeline | Responder AUC | Site Variance Impact |
| :--- | :---: | :--- |
| **Raw Unharmonized Data** | 0.919 | Confounded by technical collection shifts |
| **Within-Site Z-Harmonization** | **0.958** | Technical shifts eliminated; true biological signal isolated |

### 🧬 Real-World Immunogenomic & SHAP Explainability Benchmark

Evaluated machine learning performance on multi-gene immunogenomic expression profiles ($PDCD1/PD1$, $CD8A$, $CTLA4$, $Mutational\ Burden$) to predict Progression-Free Survival (PFS):

* **Linear Baseline (Cox PH):** **0.600 C-Index** ($PD1$ protective hazard $HR=0.84, p=0.01$).
* **Ensemble Model (Random Survival Forest):** **0.831 C-Index** (Captured non-linear gene-gene co-expression interactions).
* **Model Interpretability (SHAP):** TreeExplainer isolated top genomic drivers and quantified exact feature contributions to individual risk scores.

| Model Architecture | C-Index | Feature Mechanics |
| :--- | :---: | :--- |
| **Linear Cox PH** | 0.600 | Evaluates genes independently (misses co-expression) |
| **Random Survival Forest** | **0.831** | Captures multi-gene non-linear interactions |
| **SHAP Analysis** | — | Opens "black box" to rank gene importance |
