# 🔬 Advanced Statistical Analysis of Cancer Research Datasets

[![R](https://img.shields.io/badge/Language-R-276DC3?logo=r&logoColor=white)](https://www.r-project.org/)
[![Status](https://img.shields.io/badge/Status-Completed-success)]()
[![Course](https://img.shields.io/badge/Course-Advanced%20Statistics-blueviolet)]()
[![Institution](https://img.shields.io/badge/Institution-Universidad%20de%20Deusto-red)]()

> **Language Selection / Selección de Idioma:**  
> 🇬🇧 **English** | [🇪🇸 Leer en Castellano (Versión en Español)](README_es.md)

---

## 📌 Table of Contents
- [Overview & Objectives](#-overview--objectives)
- [Authors & Academic Context](#-authors--academic-context)
- [Repository Structure](#-repository-structure)
- [Datasets Description](#-datasets-description)
- [Methodological Modules](#-methodological-modules)
  - [1. Exploratory Data Analysis & Descriptive Statistics](#1-exploratory-data-analysis--descriptive-statistics)
  - [2. Multiple Linear Regression](#2-multiple-linear-regression)
  - [3. Binary Logistic Regression](#3-binary-logistic-regression)
  - [4. Principal Component Analysis (PCA)](#4-principal-component-analysis-pca)
  - [5. Correspondence Analysis (CA)](#5-correspondence-analysis-ca)
  - [6. Unsupervised Clustering: K-Means](#6-unsupervised-clustering-k-means)
  - [7. Hierarchical Agglomerative Clustering (HAA)](#7-hierarchical-agglomerative-clustering-haa)
  - [8. Comparative Discussion of Clustering Methods](#8-comparative-discussion-of-clustering-methods)
- [Key Findings & Clinical Insights](#-key-findings--clinical-insights)
- [Software & R Libraries](#-software--r-libraries)
- [Reproducibility & Execution Guide](#-reproducibility--execution-guide)

---

## 🔬 Overview & Objectives

This repository hosts an in-depth statistical research project focused on multivariate analysis and predictive modeling of oncological data. Developed as part of the **Advanced Statistics** (*Estadística Avanzada*) course at **Universidad de Deusto**, the primary goal of this project is to apply parametric and non-parametric statistical techniques to biomedical cancer datasets—predominantly **Breast Cancer** and **Prostate Cancer**, complemented by exploratory work on a clinical **Lung Cancer** dataset.

The investigation addresses the following core research questions:
1. **Morphological Characterization:** How do cell nucleus morphology (radius, perimeter, area, concavity, texture, compactness) differ between benign and malignant lesions?
2. **Predictive Modeling:**
   - Can we build robust linear models to predict geometric dimensions of tumors while avoiding severe multicollinearity?
   - How accurately can binary logistic regression classify tumor malignancy based on cellular features?
3. **Dimensionality Reduction:** Can high-dimensional feature spaces (e.g., 30 features from fine-needle aspirates) be effectively compressed via Principal Component Analysis (PCA) without losing critical diagnostic variance?
4. **Categorical Association:** What non-linear relationships exist between discretized morphological traits through Correspondence Analysis (CA)?
5. **Phenotypic Clustering:** Can unsupervised clustering algorithms (K-Means and Hierarchical Agglomerative Clustering) unveil latent cancer sub-types and patient groupings, both in the original feature space and in PCA-reduced space?

---

## 👥 Authors & Academic Context

- **Iker Ibarrola**
- **Enetz Quindimil**
- **Carlos Firvida**
- **Iñigo Infante**

*Institution:* **Universidad de Deusto**  
*Degree:* Computer Engineering / Data Science  
*Course:* Advanced Statistics (2nd Year, 2nd Semester)

---

## 📁 Repository Structure

```plaintext
cancerResearch/
│
├── README.md                                    # Project documentation (English)
├── README_es.md                                 # Documentación del proyecto (Castellano)
│
├── breast_cancer_data.csv                       # Wisconsin Diagnostic Breast Cancer dataset (WDBC)
├── Prostate_Cancer.csv                          # Clinical prostate cancer dataset
├── lung_cancer_data.csv                         # Synthetic clinical lung cancer dataset
│
├── DiscussionOfClusteringResults_breast_cancer.R   # K-Means vs HCA comparative synthesis (Breast)
├── DiscussionOfClusteringResults_prostate_cancer.R # K-Means vs HCA comparative synthesis (Prostate)
│
├── DESCRIPTIVE_ANALYSIS/                         # Exploratory Data Analysis (EDA)
│   ├── descriptive_analysis_breast_cancer.R      # Distribution, correlations, and plots (Breast)
│   ├── descriptive_analysis_prostate_cancer.R    # Summary statistics and distributions (Prostate)
│   └── descriptive_analysis_lung_cancer.R        # Clinical factors, demographics, and labs (Lung)
│
├── LINEAR_REGRESSION/                            # Multiple Linear Regression Modeling
│   ├── linear_regression_breast_cancer.R         # Radius Mean model, backward elimination, diagnostics
│   ├── linear_regression_prostate_cancer.r       # Compactness model, ANOVA, prediction intervals
│   └── other_LRmodels_breast_cancer.R            # Perimeter/Area models & 21-variable comparison
│
├── LOGISTIC_REGRESSION/                          # Binary Classification Modeling
│   ├── logistic_regression_breast_cancer.R       # Diagnosis classification, Caret matrix, ROC/AUC
│   └── logistic_regression_prostate_cancer.R     # Predictor selection, sigmoid fits, cut-off tuning
│
├── PCA/                                          # Principal Component Analysis
│   ├── PCA_breast_cancer.R                       # Dual-model PCA (30 features vs 10 means), biplots
│   └── PCA_prostate_cancer.R                     # Scaled PCA, duality, patient-variable vectors
│
├── CA/                                           # Correspondence Analysis
│   ├── CA_breast_cancer.R                        # Quartile discretization, Chi-square test, 2D map
│   ├── CA_prostate_cancer.R                      # Standard deviation discretization, profile analysis
│   └── TEST_CA_Multiple_variable_combination.R   # Multi-variable 3-way discretization experiment
│
├── K-MEANS/                                      # Unsupervised K-Means Clustering
│   ├── K-means_breast_cancer.R                   # WCSS/Silhouette, K=15, PCA vs Original, heatmaps
│   └── K-Means_prostate_cancer.R                 # K=3 clusters, variable-cluster correlations
│
└── HAA/                                          # Hierarchical Agglomerative Clustering
    ├── HAA_Breast_Cancer.R                       # Complete linkage, dendrograms, cluster profiles
    └── HAA_prostate_cancer.r                     # Complete linkage, height/k cuts, contingency heatmaps
```

---

## 📊 Datasets Description

### 1. Wisconsin Diagnostic Breast Cancer (WDBC) (`breast_cancer_data.csv`)
- **Instances:** 569 patients (357 Benign, 212 Malignant).
- **Features:** 32 variables:
  - `id`: Unique identifier (discarded during preprocessing).
  - `diagnosis`: Pathological diagnosis (`B` = Benign, `M` = Malignant).
  - 30 real-valued continuous features computed from digitized images of Fine Needle Aspirates (FNA) of breast masses, covering 10 nuclear morphometric properties across three statistics:
    - **Mean** (`_mean`): Central tendency of cell nuclear characteristics.
    - **Standard Error** (`_se`): Variability across measured nuclei.
    - **Worst / Largest** (`_worst`): Mean of the three largest values per image.
  - **Morphometric Properties:** Radius, Texture, Perimeter, Area, Smoothness, Compactness, Concavity, Concave Points, Symmetry, Fractal Dimension.
- **Data Quality:** Zero missing values. Approximately 2% of samples display `concavity_mean = 0`, an uncommon but verified physiological occurrence in strictly non-concave benign cells.

### 2. Prostate Cancer Dataset (`Prostate_Cancer.csv`)
- **Instances:** 100 clinical records (62 Malignant, 38 Benign).
- **Features:** 10 attributes:
  - `id`: Patient ID.
  - `diagnosis_result`: Clinical diagnosis (`M` / `B`).
  - 8 morphological and structural metrics: `radius`, `texture`, `perimeter`, `area`, `smoothness`, `compactness`, `symmetry`, and `fractal_dimension`.
- **Data Quality:** Clean continuous measurements; zero missing values.

### 3. Clinical Lung Cancer Dataset (`lung_cancer_data.csv`)
- **Instances:** 23,658 patients.
- **Features:** 38 clinical, epidemiological, and laboratory attributes:
  - Demographics: Age, Gender, Ethnicity, Insurance Type.
  - Lifestyle & History: Smoking History, Smoking Pack-Years, Family History.
  - Disease Status & Treatment: Tumor Size (mm), Tumor Location, Cancer Stage (I–IV), Treatment Modality, Survival Months.
  - Comorbidities (Diabetes, Hypertension, Heart Disease, Chronic Lung Disease, Kidney Disease, Autoimmune Disease).
  - Vital Signs & Blood Chemistry: Systolic/Diastolic BP, Hemoglobin, WBC, Platelets, Albumin, ALP, ALT, AST, Creatinine, LDH, Calcium, Potassium, Glucose.
- **Role in Project:** Benchmark for large-scale exploratory data analysis, multivariate contingency profiling, and factor associations.

---

## 🔬 Methodological Modules

### 1. Exploratory Data Analysis & Descriptive Statistics
*Directory: [`DESCRIPTIVE_ANALYSIS/`](DESCRIPTIVE_ANALYSIS/)*

- **Data Wrangling:** Stripped extraneous identifiers (`id`, `Patient_ID`), mapped binary labels to informative factors (`benign`, `malign`), and verified data completeness with `colSums(is.na(data))`.
- **Univariate Analytics:** Calculated parametric and non-parametric summaries using `summary()` and `pastecs::stat.desc()` (mean, median, standard deviation, variance, IQR, percentiles).
- **Multicollinearity Discovery:** Pearson correlation matrices revealed near-perfect collinearity between geometric features:
  - $\text{cor}(\text{radius\_mean}, \text{perimeter\_mean}) > 0.99$
  - $\text{cor}(\text{radius\_mean}, \text{area\_mean}) > 0.98$
  - $\text{cor}(\text{perimeter\_mean}, \text{area\_mean}) > 0.98$
  - Strong correlations ($> 0.85$) between each metric's `mean` and `worst` version.
- **Visual Exploration:** Boxplots, violin plots, and stratified dotplots built with `ggplot2` and `lattice` demonstrated marked morphological divergence between benign and malignant cases.
- **Normality Assessment:** Quantile-Quantile (`car::qqPlot`) plots and skewness calculations indicated significant non-normality in raw distributions, motivating data transformations and robust parametric testing.

---

### 2. Multiple Linear Regression
*Directory: [`LINEAR_REGRESSION/`](LINEAR_REGRESSION/)*

#### Breast Cancer Models ([`linear_regression_breast_cancer.R`](LINEAR_REGRESSION/linear_regression_breast_cancer.R))
- **Response Selection:** `radius_mean` was selected as the continuous response. An ANOVA test confirmed massive between-group divergence by diagnosis ($F$-test $p = 8.47 \times 10^{-96}$).
- **Predictor Filtering:** Removed collinear geometric attributes (`area`, `perimeter`, all `_worst` variables, and correlated `_se` variables) to prevent variance inflation.
- **Stepwise Backward Elimination:** Starting from an initial multi-variable model, predictors with $p > 0.05$ were sequentially removed (`symmetry_se` $\rightarrow$ `texture_se` $\rightarrow$ `texture_mean`).
- **Final Model:**
  $$\text{radius\_mean} \sim \text{smoothness\_mean} + \text{compactness\_mean} + \text{concave.points\_mean} + \text{symmetry\_mean} + \text{fractal\_dimension\_mean} + \text{smoothness\_se}$$
- **Hypothesis Testing:**
  - Overall model significance: $F$-test yielded $p < 2.2 \times 10^{-16}$.
  - Nested Model ANOVA: Compared the reduced model to the full model, verifying no statistically significant loss in explanatory performance ($p > 0.05$).
- **Diagnostics & Assumptions:**
  - Residuals vs. Fitted values confirmed linearity and homoscedasticity.
  - Residual skewness ($0.328$) verified near-symmetric, approximately normal errors.
  - Cook's distance analysis identified high-leverage observation `214`; refitting without observation 214 showed model coefficient stability and negligible adjusted $R^2$ variation.
- **Interval Validation:**
  - 99% Confidence intervals on training data: ~20% captured within narrow confidence bands.
  - 95% Prediction intervals on an independent 20% holdout test set: **>90% test coverage**.

#### Alternative Breast Cancer Models ([`other_LRmodels_breast_cancer.R`](LINEAR_REGRESSION/other_LRmodels_breast_cancer.R))
- Modeled `area_mean` and `perimeter_mean`, as well as a full 21-variable backward selection model.
- Demonstrated that all four linear formulations achieved virtually identical test-set prediction interval accuracy (>90-93%), confirming that geometric consistency across nuclear measurements is preserved regardless of chosen response.

#### Prostate Cancer Model ([`linear_regression_prostate_cancer.r`](LINEAR_REGRESSION/linear_regression_prostate_cancer.r))
- Response variable: `compactness` (ANOVA $p = 5.10 \times 10^{-8}$ across diagnosis groups).
- Backward elimination retained: `perimeter`, `area`, `symmetry`, and `fractal_dimension`.
- Test prediction interval coverage: **100% on unseen test observations**.

---

### 3. Binary Logistic Regression
*Directory: [`LOGISTIC_REGRESSION/`](LOGISTIC_REGRESSION/)*

#### Breast Cancer Classification ([`logistic_regression_breast_cancer.R`](LOGISTIC_REGRESSION/logistic_regression_breast_cancer.R))
- **Objective:** Classify tumors as `benign` ($0$) or `malign` ($1$).
- **Visual Variable Screening:** Violin plots with integrated boxplots isolated variables showing maximal separation between benign and malignant classes (e.g., `radius_mean`, `compactness_mean`, `concavity_mean`).
- **Model Fitting:** Fitted Generalized Linear Models (GLM) with `family = binomial(link = "logit")`. Backward elimination retained:
  $$\text{logit}(P(\text{malign})) = \beta_0 + \beta_1(\text{texture\_mean}) + \beta_2(\text{compactness\_mean}) + \beta_3(\text{concave.points\_mean}) + \beta_4(\text{radius\_mean})$$
- **Evaluation Metrics (Threshold = 0.5):**
  - **Accuracy:** **94.38%**
  - **Sensitivity (Recall for Malignant):** **96.64%**
  - **Specificity (True Negative Rate):** High discriminative accuracy on benign cases.
  - **ROC & AUC:** Computed via `pROC::roc()`; the ROC curve yielded an outstanding AUC approaching 0.98.

#### Prostate Cancer Classification ([`logistic_regression_prostate_cancer.R`](LOGISTIC_REGRESSION/logistic_regression_prostate_cancer.R))
- Univariate sigmoid curve overlay on raw scatter data demonstrated why features like `perimeter` and `compactness` provide superior logistic fits compared to `radius`.
- Stepwise regression identified `compactness` and `fractal_dimension` as core predictors.
- Plotted the sensitivity vs. specificity trade-off across varying probability thresholds to identify the optimal classification cut-off point.

---

### 4. Principal Component Analysis (PCA)
*Directory: [`PCA/`](PCA/)*

#### Dual Breast Cancer Analysis ([`PCA_breast_cancer.R`](PCA/PCA_breast_cancer.R))
- **Comparative Design:** To resolve the trade-off between information richness and multicollinearity noise, two separate PCA models were fitted and compared using `FactoMineR::PCA(scale.unit = TRUE)`:
  1. **Full Model (30 variables):** All mean, se, and worst metrics.
  2. **Means Model (10 variables):** Nuclear means only.
- **Dimensionality Selection & Scree Plots:**
  - Kaiser Criterion ($\lambda > 1$): 6 components for the full model; 2 components for the means model.
  - Elbow Rule: In both models, an elbow occurred at Component 3.
  - The first two principal components explained **63%** of total variance in the full model and **~80%** in the means model.
- **Factor Loadings & Correlation Circle:**
  - **PC1:** Strongest positive correlations ($r > 0.80$) with nuclear size and shape metrics (`radius_mean`, `perimeter_mean`, `area_mean`, `compactness_mean`, `concavity_mean`, `concave.points_mean`).
  - **PC2:** Predominantly aligned with `fractal_dimension_mean` ($r \approx 0.90$) and texture properties.
- **Quality of Representation ($\cos^2$) & Contributions ($\text{contrib}$):** Verified that leading variables are projected closely onto the correlation circle boundary.
- **Clinical Projections:**
  - Individual coordinates colored by diagnosis showed striking cluster separation along **PC1**: benign tumors occupy negative PC1 values, while malignant tumors populate positive PC1 values.
  - Confirmed via ANOVA on PC1 coordinates: $F$-test $p = 3.13 \times 10^{-120}$.

#### Prostate Cancer PCA ([`PCA_prostate_cancer.R`](PCA/PCA_prostate_cancer.R))
- Reduced 8 continuous features down to 2 principal components explaining **62.93%** of variance.
- Biplots and duality representations illustrated the geometric alignment between individual patient coordinates and variable projection vectors.

---

### 5. Correspondence Analysis (CA)
*Directory: [`CA/`](CA/)*

While PCA handles continuous spaces, Correspondence Analysis explores associations across categorical levels.

#### Breast Cancer CA ([`CA_breast_cancer.R`](CA/CA_breast_cancer.R))
- **Discretization:** Transformed continuous features into 4 ordinal quartile tiers (*very low*, *low*, *high*, *very high*):
  - `radius_mean_cat` (tumor size).
  - `smoothness_mean_cat` (tumor surface texture).
- **Contingency & Expected Tables:**
  - Strong positive association found between `very high radius` and `very high smoothness` (observed = 45 vs. expected = 35.44).
  - Pronounced negative association (repulsion) between `very high radius` and `very low smoothness` (observed = 17 vs. expected = 35.69).
- **Independence Test:** Pearson's $\chi^2$ test yielded $p < 0.05$, firmly rejecting independence.
- **2D CA Factorial Map:** Mapped row and column categories, illustrating structural groupings between morphological size tiers and boundary smoothness.

#### Prostate Cancer CA ([`CA_prostate_cancer.R`](CA/CA_prostate_cancer.R) & [`TEST_CA_Multiple_variable_combination.R`](CA/TEST_CA_Multiple_variable_combination.R))
- Discretized continuous features using standard deviation thresholds ($< \mu - \sigma$, $[\mu - \sigma, \mu + \sigma]$, $> \mu + \sigma$) into *low*, *normal*, and *high* categories.
- Evaluated row/column profiles, Pearson residuals, cell contributions, and 2D inertia projections.

---

### 6. Unsupervised Clustering: K-Means
*Directory: [`K-MEANS/`](K-MEANS/)*

#### Breast Cancer K-Means ([`K-means_breast_cancer.R`](K-MEANS/K-means_breast_cancer.R))
- **Dual-Space Clustering:** Executed K-Means both directly on standardized original variables and on PCA-transformed coordinates (PC1–PC2).
- **Cluster Number Selection:**
  - Tested $k \in [1, 50]$ with `nstart = 10`.
  - WCSS elbow curves and silhouette scores evaluated; selected $k = 15$ to explore granular tumor subtypes.
- **Heatmap Cross-Tabulation:** Constructed a confusion heatmap comparing cluster assignments between original variables and PCA space. Several clusters showed direct 1-to-1 equivalence (e.g., Cluster 6 Original $\equiv$ Cluster 5 PCA; Cluster 3 Original $\equiv$ Cluster 4 PCA), proving that PCA dimensionality reduction preserved essential clustering geometry.
- **Cluster Phenotyping:**
  - Faceted violin plots with `scico::lajolla` palette characterized the distribution of each feature across clusters.
  - Overlaying pathological diagnosis onto clusters in PCA space revealed:
    - **5 pure malignant clusters** (high radius, high concavity, high PC1).
    - **6 pure benign clusters** (low radius, low concavity, low PC1).
    - **4 mixed border clusters**, representing ambiguous or transitional histological cases.

#### Prostate Cancer K-Means ([`K-Means_prostate_cancer.R`](K-MEANS/K-Means_prostate_cancer.R))
- Optimal $k = 3$ determined using WCSS elbow and silhouette metrics.
- Projected clusters in PCA space: identified **2 distinct malignant sub-clusters** and **1 uniform benign cluster**.

---

### 7. Hierarchical Agglomerative Clustering (HAA)
*Directory: [`HAA/`](HAA/)*

- **Distance & Linkage:** Computed Euclidean distance matrices (`stats::dist`) and applied hierarchical agglomerative clustering via **complete linkage** (`method = "complete"`).
- **Dendrogram Partitioning:** Evaluated horizontal cutting heights (`h`) and vertical cluster cuts (`k = 2` for original variables; `k = 4` for PCA space).
- **Cluster Assignment Heatmaps:** Compared dendrogram assignments between original variables and PCA components, discovering that PCA splits the broad primary cluster into nuanced sub-phenotypes.
- **Feature Correlation:** Calculated point-biserial correlations between binary cluster membership vectors and continuous features to determine the dominant morphometric drivers per branch.

---

### 8. Comparative Discussion of Clustering Methods
*Scripts: [`DiscussionOfClusteringResults_breast_cancer.R`](DiscussionOfClusteringResults_breast_cancer.R) & [`DiscussionOfClusteringResults_prostate_cancer.R`](DiscussionOfClusteringResults_prostate_cancer.R)*

The root comparison scripts synthesize the findings of K-Means versus Hierarchical Clustering (HCA):
- When fixing $k = 3$ on PCA coordinates, both algorithms demonstrate general convergence on primary groups, but reveal notable boundary divergences:
  - In Prostate Cancer, Cluster 1 of K-Means corresponds identically to Cluster 2 of HCA.
  - Intermediate and borderline observations are assigned differently due to the differing mathematical objectives: K-Means minimizes intra-cluster variance around dynamic centroids, whereas complete-linkage HCA constructs compact, spherical clusters based on maximum pairwise distance.

---

## 💡 Key Findings & Clinical Insights

1. **Size and Concavity Are Definitive Malignancy Drivers:** In both linear models, logistic regression, and PCA, metrics associated with tumor radius, perimeter, and concave points consistently exhibited the strongest statistical association with malignancy ($p < 10^{-90}$).
2. **PCA Successfully Compress Diagnostics:** Reducing 30 breast cancer features down to 2 principal components retained over **63%** of total variance (and **~80%** when focusing on mean features), with PC1 providing near-linear separation between benign and malignant cases ($p = 3.13 \times 10^{-120}$).
3. **Logistic Regression Yields High Sensitivity:** The reduced 4-predictor logistic model achieved an accuracy of **94.38%** and a sensitivity of **96.64%**, minimizing critical false-negative diagnoses.
4. **Unsupervised Identification of Borderline Lesions:** K-Means clustering ($k = 15$) autonomously segmented lesions into discrete benign and malignant phenotypes, while isolating 4 intermediate clusters where benign and malignant samples overlap—highlighting cases where morphological imaging alone warrants biopsy confirmation.

---

## 🛠 Software & R Libraries

The project was executed in **R (version 4.x)** using RStudio. The following packages are required:

| Category | R Packages |
| :--- | :--- |
| **Data Manipulation** | `dplyr`, `tidyr`, `reshape2`, `glue`, `pastecs` |
| **Data Visualization** | `ggplot2`, `lattice`, `plotrix`, `patchwork`, `plotly`, `fields`, `scico` |
| **Statistical Modeling & Tests** | `car`, `moments`, `pROC`, `caret`, `ResourceSelection` |
| **Multivariate & Clustering** | `FactoMineR`, `factoextra`, `stats` |

---

## 🚀 Reproducibility & Execution Guide

### 1. Clone the Repository
```bash
git clone https://github.com/ikeiba/cancerResearch.git
cd cancerResearch
```

### 2. Install Required R Packages
Open an R session or RStudio and run:
```R
required_packages <- c(
  "dplyr", "tidyr", "reshape2", "glue", "pastecs",
  "ggplot2", "lattice", "plotrix", "patchwork", "plotly", "fields", "scico",
  "car", "moments", "pROC", "caret", "ResourceSelection",
  "FactoMineR", "factoextra"
)

new_packages <- required_packages[!(required_packages %in% installed.packages()[, "Package"])]
if(length(new_packages) > 0) install.packages(new_packages)
```

### 3. Run Analysis Scripts
Set the working directory to the repository root:
```R
setwd("path/to/cancerResearch")
```

Execute any module directly in R:
```R
# 1. Descriptive Analysis
source("DESCRIPTIVE_ANALYSIS/descriptive_analysis_breast_cancer.R")

# 2. Linear Regression
source("LINEAR_REGRESSION/linear_regression_breast_cancer.R")

# 3. Logistic Regression
source("LOGISTIC_REGRESSION/logistic_regression_breast_cancer.R")

# 4. Principal Component Analysis (PCA)
source("PCA/PCA_breast_cancer.R")

# 5. Correspondence Analysis (CA)
source("CA/CA_breast_cancer.R")

# 6. K-Means Clustering
source("K-MEANS/K-means_breast_cancer.R")

# 7. Hierarchical Agglomerative Clustering
source("HAA/HAA_Breast_Cancer.R")

# 8. Comparative Clustering Synthesis
source("DiscussionOfClusteringResults_breast_cancer.R")
```

---

<div align="center">
  <sub>Developed for the Advanced Statistics course at Universidad de Deusto &bull; 2025</sub><br>
  <sub><a href="README_es.md">🇪🇸 Cambiar a versión en Castellano</a></sub>
</div>

