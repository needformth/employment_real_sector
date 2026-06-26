# Impact of Real Sector Development on Employment in Russian Regions

## Overview

This project investigates the relationship between **real sector development** and **employment levels** across Russian regions. Using a rich dataset of 87 regions over 6 years (2018–2023), the study explores how macroeconomic and industrial indicators influence regional employment.

The analysis combines **hierarchical clustering**, **regression modeling**, **Granger causality testing**, and **dimensionality reduction** to uncover structural patterns and causal relationships.

---

## Project Objectives

- Identify groups of regions with similar economic profiles using clustering.
- Test for Granger-causal relationships between real-sector variables and employment.
- Build interpretable regression models to explain employment variation across clusters.
- Provide data-driven insights for regional policy and labor market analysis.

---

## Dataset

### Indicators

| Variable | Description | Unit |
|----------|-------------|------|
| `industry_index` | Industrial production index | % (previous year = 100%) |
| `capital_investments` | Share of fixed capital investments in GRP | % |
| `load_capacity_grp` | Freight intensity of GRP | ton‑km / USD |
| `secondary_sector` | Share of manufacturing in GRP | % |
| `labour_productivity` | Labour productivity growth | % |
| `employment` | Employment rate | % of working‑age population |

Each variable is observed for **87 Russian regions** (including federal subjects) over the period **2018–2023**. Data are sourced from official Russian statistics (Rosstat).

---

## Methodology

### 1. Data Preprocessing

- Outliers were capped at the 10th and 90th percentiles per year to reduce extreme values.
- All variables were averaged over the 6‑year period to obtain a cross‑sectional profile for each region.
- Standardization (Z‑score) was applied before clustering and PCA.

### 2. Hierarchical Clustering

- **Linkage method**: Ward’s minimum variance (chosen after comparing Ward, complete, average, and single linkage).
- **Distance metric**: Euclidean distance on standardized data.
- The dendrogram was cut to form **3 clusters** based on economic characteristics.

### 3. Cluster Profiling

For each cluster, average indicator values were computed and visualised using heatmaps and bar charts. Clusters were interpreted as:

- **Cluster 1** – Resource‑investment regions (high investment, low freight intensity, moderate employment).
- **Cluster 2** – Classic industrial regions (strong manufacturing, high labour productivity, moderate investment).
- **Cluster 3** – Peripheral/intermediate regions (below‑average industrial and employment indicators).

### 4. Granger Causality Testing

For each cluster, Granger causality tests (with lag 1) were performed to check whether changes in real‑sector indicators *precede* changes in employment.

The following relationships were found statistically significant (p < 0.15) for Cluster 3:

- **Freight intensity** → Employment (p = 0.0099)
- **Labour productivity** → Employment (p = 0.0507)

Other clusters showed weaker causal links, suggesting different regional dynamics.

### 5. Regression Modeling

Linear regression models were built for each cluster to explain employment using combinations of real‑sector predictors. Model selection was based on:

- **Adjusted R²**
- **Statistical significance of coefficients** (p < 0.15)
- **Multicollinearity check** (VIF)

The best‑performing models per cluster are summarised below.

---

## Key Results

### Cluster Profiles (Average values)

| Cluster | Regions | Industry Index | Capital Inv. | Freight Intensity | Manufacturing | Labour Prod. | Employment |
|---------|---------|---------------|--------------|-------------------|---------------|--------------|------------|
| **1**   | 26      | 104.4         | 26.5%        | 0.11              | 6.0%          | 102.6%       | 59.0%      |
| **2**   | 24      | 105.9         | 19.4%        | 0.20              | 24.2%         | 103.1%       | 59.4%      |
| **3**   | 37      | 102.5         | 19.1%        | 0.18              | 17.7%         | 101.7%       | 57.6%      |

- **Cluster 1** (e.g., Kursk, Nenets, Caucasian republics) – high investment and industrial growth, but low manufacturing share.
- **Cluster 2** (e.g., Bryansk, Vladimir, Moscow region) – strong manufacturing and productivity.
- **Cluster 3** (e.g., Belgorod, Vologda, Komi) – below‑average on most indicators.

---

### Granger Causality (lag 1)

| Cluster | Variable | p‑value (F‑test) |
|---------|----------|------------------|
| 1       | none     | >0.15            |
| 2       | none     | >0.15            |
| **3**   | **Freight intensity** | **0.0099** |
| **3**   | **Labour productivity** | **0.0507** |

For Cluster 3, freight intensity and labour productivity Granger‑cause employment, indicating that structural changes in these variables precede changes in employment rates.

---

### Regression Models (final selection)

| Cluster | Predictors | Adj. R² | Key coefficients |
|---------|------------|---------|-------------------|
| **1**   | Industry index, Manufacturing | 67.5% | Industry: +0.232 (p=0.069), Manufacturing: +1.876 (p=0.057) |
| **2**   | Industry, Investments, Freight intensity, Manufacturing | ~100%* | All significant (p<0.05) |
| **3**   | Freight intensity, Manufacturing, Labour productivity | 91.4% | Freight: -28.8 (p=0.17), Manufacturing: -1.51 (p=0.12), Labour prod: +0.47 (p=0.06) |

*Note: The near‑perfect fit for Cluster 2 suggests overfitting due to limited observations; results should be interpreted with caution.*

The models show that:
- In **Cluster 1**, industrial output and manufacturing share positively influence employment.
- In **Cluster 2**, all real‑sector variables jointly explain employment, but the model may be over‑specified.
- In **Cluster 3**, labour productivity positively affects employment, while freight intensity and manufacturing share show negative coefficients (possibly reflecting structural inefficiencies).

---

### PCA Visualization

Principal Component Analysis (PCA) was applied to the standardized regional profiles. The first two components explain ~60% of variance and clearly separate clusters:

- **Cluster 1** (high investment) appears in the upper‑right.
- **Cluster 2** (manufacturing‑oriented) occupies the left‑center.
- **Cluster 3** (peripheral) is spread across the lower area.

All regions are labelled on the plot for easy identification.

---

## Skills Demonstrated

### Data Science & Econometrics
- **Time‑series analysis** (Granger causality)
- **Cluster analysis** (hierarchical, Ward linkage)
- **Regression modeling** (OLS, variable selection)
- **Dimensionality reduction** (PCA)
- **Multicollinearity assessment** (VIF)
- **Outlier treatment** (percentile capping)

### Programming & Tools
- **Python** (pandas, numpy, matplotlib, seaborn)
- **scikit‑learn** (StandardScaler, PCA)
- **statsmodels** (OLS, Granger causality, VIF)
- **scipy** (hierarchical clustering, distance metrics)
- **Jupyter Notebook** for interactive analysis

### Data Handling
- Reading/writing Excel files
- Data cleaning and transformation
- Aggregation and grouping
- Standardization and normalization

---

## Technologies

- Python 3.8+
- Pandas, NumPy
- Matplotlib, Seaborn
- Scikit‑learn
- Statsmodels
- SciPy
- Jupyter Notebook

---

## How to Run

1. Clone the repository.
2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
3. Open `analysis.ipynb` in Jupyter.
4. Run all cells sequentially.

> The notebook includes comprehensive comments (in Russian) and can be adapted for other regional datasets.

---

## Conclusions

- **Regional heterogeneity** is strong: three distinct clusters emerge based on real‑sector structure.
- **Causal links** between real‑sector development and employment are cluster‑specific – not all regions follow the same logic.
- **Labour productivity** and **freight intensity** appear as leading indicators in peripheral regions.
- **Manufacturing share** and **industrial output** are important for industrial and investment‑oriented regions.
- The results suggest that **one‑size‑fits‑all policies** may be ineffective; targeted regional strategies are needed.

---

## Future Work

- Extend the analysis with more years of data.
- Include additional socio‑demographic controls (e.g., education, migration).
- Apply panel data methods (fixed effects, random effects) to capture regional and time heterogeneity.
- Use machine learning (e.g., random forests) to identify non‑linear relationships.
