 # 🍷 Data-Driven Analysis of Wine Chemistry & Consumer Quality Scores

A comprehensive, end-to-end data science case study exploring the chemical determinants of wine quality across red and white wines. This project combines exploratory analysis, unsupervised learning, and machine learning regression to answer a central question:

> **Can physicochemical properties measured in a laboratory reliably predict how a wine will be scored by human experts?**

---

## Project Objectives

| # | Objective |
|---|-----------|
| 1 | Identify which physicochemical features correlate most strongly with quality scores |
| 2 | Apply PCA to reduce dimensionality and surface interpretable quality dimensions |
| 3 | Segment wines into distinct chemical-performance profiles using k-means clustering |
| 4 | Derive actionable chemical benchmarks for high-quality clusters |
| 5 | Train and evaluate ML regression models to predict quality from chemistry alone |
| 6 | Quantify how much of wine quality can be explained by chemistry vs. human perception |

> **Note on target variable:** Quality scores are used as a proxy for overall consumer preference. These scores were assigned by expert panels and carry inherent subjectivity. Full methodology and assumptions are documented in the Jupyter notebook.

---

## Datasets

| Dataset | Rows | Source |
|---------|------|--------|
| Red Wine (`winequality-red.csv`) | 1,599 | UCI Machine Learning Repository |
| White Wine (`winequality-white.csv`) | 4,898 | UCI Machine Learning Repository |
| Combined (`wine_combined.csv`) | 6,497 | Cleaned & labeled for dashboard use |

**Source:** Cortez, P., Cerdeira, A., Almeida, F., Matos, T., & Reis, J. (2009). [Wine Quality Dataset](https://archive.ics.uci.edu/dataset/186/wine+quality). UCI Machine Learning Repository.

---

## ⚙️ Workflow & Techniques

| Phase | Technique | Purpose |
|-------|-----------|---------|
| Data Cleaning & EDA | pandas, numpy, seaborn, matplotlib | Distributions, missing values, outliers, correlations |
| Correlation Analysis | pandas, seaborn heatmaps | Quantify feature relationships with chemical context |
| Dimensionality Reduction | PCA (scikit-learn) | Compress chemistry into two interpretable quality axes |
| Clustering | k-Means, silhouette score, elbow method | Segment wines by chemical-performance profile |
| Cluster Profiling | Groupby, boxplots, countplots | Link clusters to quality scores and chemistry |
| Threshold Benchmarking | Aggregation, feature selection | Define actionable chemical targets per wine type |
| ML — Ridge Regression | scikit-learn, StandardScaler | Linear baseline; interpretable coefficient direction |
| ML — Random Forest | scikit-learn RandomForestRegressor | Non-linear relationships, feature importance |
| ML — XGBoost | XGBRegressor | Sequential error correction; best overall performance |

---

## Key Results & Insights

### 1. Chemistry Correlates Strongly with Quality

Most wines cluster around scores of 5–6 on a 1–10 scale. Features most associated with higher quality scores:

- **Red Wine:** High alcohol, high sulphates, low volatile acidity, low chlorides, high citric acid
- **White Wine:** High alcohol, high pH, low density, low chlorides, low total sulfur dioxide

---

### 2. PCA Surfaces Two Core Quality Dimensions

| Component | What It Captures | Key Features |
|-----------|-----------------|--------------|
| **PC1 — Ripeness & Fermentation Efficiency** | Grape maturity and process completeness | High alcohol, low density, high citric acid, high sulphates, low volatile acidity |
| **PC2 — Processing & Stabilization Intensity** | Level of intervention and preservation | High SO₂, more residual sugar, higher density |

**Interpretation:** Wines with riper grapes and cleaner fermentations (high PC1, low PC2) consistently receive higher quality scores across both wine types.

---

### 3. Clustering Reveals Distinct Quality Profiles

**Red Wine — Cluster 0 (Highest Performing)**
- Mean quality score: **5.95** | Largest share of scores ≥ 7
- Profile: High ripeness (high PC1), low stabilization intensity (low PC2)
- Interpretation: Riper fruit + clean fermentation conditions

**White Wine — Cluster 0 (Highest Performing)**
- Mean quality score: **6.17** | Largest share of scores ≥ 7
- Profile: Lower ripeness (low PC1), low stabilization intensity (low PC2)
- Interpretation: Neat processing and minimal intervention drive quality more than raw ripeness

💡 **Cross-type insight:** In both wine categories, the clusters with the least processing/stabilization intensity consistently achieved the highest scores — suggesting that clean, minimal-intervention winemaking is rewarded by expert panels regardless of grape variety.

---

### 4. Chemical Benchmarks for High-Quality Production

| Variable | Red Wine Target | White Wine Target |
|----------|----------------|------------------|
| Alcohol (%) | > 10.6 | > 11.2 |
| Sulphates (g/L) | > 0.75 | > 0.51 |
| Citric Acid (g/L) | > 0.48 | > 0.28 |
| Volatile Acidity (g/L) | < 0.41 | < 0.28 |
| Chlorides (g/L) | < 0.10 | < 0.04 |
| pH | > 3.18 | > 3.31 |
| Density | < 0.9978 | < 0.9920 |
| Total SO₂ (mg/L) | < 30 | < 123 |
| Residual Sugar (g/L) | < 2.6 | < 3.4 |

---

### 5. Machine Learning — Can Chemistry Predict Quality?

Three regression models were trained and evaluated on the combined dataset (80/20 train-test split):

| Model | R² | RMSE | MAE |
|-------|----|------|-----|
| Ridge Regression | 0.27 | 0.7357 | 0.5644 |
| Random Forest | 0.46 | 0.6308 | 0.4758 |
| **XGBoost** | **0.51** | **0.6039** | **0.4412** |

**Metric definitions:**
- **R²** — proportion of quality variance explained by the model (higher = better)
- **RMSE** — average prediction error in quality points, penalising large mistakes extra (lower = better)
- **MAE** — average absolute error in quality points, straightforward to interpret (lower = better)

**XGBoost is the best-performing model**, achieving the highest R² and lowest error across both RMSE and MAE.

#### What the models agree on — consistent chemical drivers across all three:

1. **Alcohol** — the single strongest predictor in every model. A proxy for grape ripeness and fermentation efficiency: high alcohol means grapes were harvested at peak maturity and the fermentation ran clean and complete.

2. **Volatile Acidity** — consistently the top negative driver. Signals fermentation stress, oxidation, or unstable storage. A chemical marker of what went wrong somewhere in the process.

3. **Free SO₂ and Sulphates** — positive contributors across models, reflecting deliberate quality-oriented winemaking: antimicrobial protection and oxidation prevention from fermentation through to bottling.

4. **Density** — consistent negative driver; a composite signal for lower alcohol yield and incomplete fermentation.

#### The 50/50 finding:

> **~50% of wine quality variation is explained by chemistry. The remaining ~50% reflects individual human perception** — personal taste preferences, tasting context, and the irreducible subjectivity of sensory experience.

This is not a modeling limitation. It is an honest reflection of what laboratory measurements can and cannot explain about human judgment. The chemistry provides a strong, measurable foundation for quality — the rest belongs to the taster.

---

## 💡 Why This Matters

- **Objective quality control:** Physicochemical measurements offer a scalable, data-driven alternative to purely subjective sensory evaluation
- **Actionable production targets:** The benchmarks derived here give winemakers specific, measurable parameters to monitor and optimize
- **Cross-industry applicability:** The analytical approach — EDA → PCA → clustering → ML regression — is directly transferable to food & beverage quality control, manufacturing process optimization, and any domain where product quality needs to be quantified from laboratory data

---

## 📦 Repository Structure

```
wine-quality-analysis/
│
├── Wine_Quality_Analysis.ipynb     # Full end-to-end analysis notebook
├── winequality-red.csv             # Red wine dataset (UCI)
├── winequality-white.csv           # White wine dataset (UCI)
├── wine_combined.csv               # Cleaned & labeled combined dataset
├── images/                         # Plots and visualizations
│   ├── correlation_heatmap_red.png
│   ├── correlation_heatmap_white.png
│   ├── red_wine_clusters.png
│   ├── white_wine_clusters.png
│   ├── ridge_coefficients.png
│   ├── rf_importance.png
│   ├── xgb_importance.png
│   └── model_comparison.png
└── README.md                       # Project documentation
```

---

## 🚀 How to Run

1. Clone this repository
2. Install dependencies:
```bash
pip install pandas numpy matplotlib seaborn scikit-learn xgboost jupyter
```
3. Download datasets from [UCI](https://archive.ics.uci.edu/dataset/186/wine+quality) if not present
4. Run `Wine_Quality_Analysis.ipynb` cell by cell to reproduce the full analysis

---

## 📜 References

- [Wine Quality Dataset — UCI Machine Learning Repository](https://archive.ics.uci.edu/dataset/186/wine+quality)
- Cortez, P., Cerdeira, A., Almeida, F., Matos, T., & Reis, J. (2009). Wine Quality. *UCI Machine Learning Repository*. https://doi.org/10.24432/C56S3T

---

## 👨‍💻 Author

**Renato Silva** — Data Analyst

[LinkedIn](https://www.linkedin.com/in/) | [GitHub](https://github.com/RenatoMateo)

---

*"The discovery of a good wine is increasingly better for mankind than the discovery of a new star."*
— Leonardo da Vinci 🍇