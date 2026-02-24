 # 🍷 Wine Quality Analysis Project

Welcome to the **Wine Quality Analysis** project! This repository contains a comprehensive, end-to-end data science case study exploring the drivers of wine quality using advanced statistical and machine learning techniques. In this project, I focus on identifying which physicochemical characteristics and chemical profiles correlate most with higher perceived wine quality, using large, real-world datasets for both red and white wines.

---

## Project Objectives

- **Analyze**: Uncover the chemical features that impact expert/consumer wine quality ratings.
- **Segment**: Use unsupervised learning to cluster wines by chemical profile and relate these segments to quality scores.
- **Benchmark**: Define clear, actionable chemical thresholds that winemakers can target to improve product quality.
- **Predict**: Apply machine learning models to predict wine quality scores using only laboratory measurements.

---

## Key Datasets

- **Red Wine**: `winequality-red.csv`  
- **White Wine**: `winequality-white.csv`  
  Datasets from the [UCI Machine Learning Repository](https://archive.ics.uci.edu/dataset/186/wine+quality), containing 12 physicochemical features and expert quality ratings for thousands of wines.

---

## ⚙️ Core Techniques and Workflow

| Step                               | Technique / Library                                     | Purpose                                         |
|-------------------------------------|---------------------------------------------------------|-------------------------------------------------|
| **Data Cleaning & EDA**             | pandas, numpy, seaborn, matplotlib                      | Explore distributions, missing values, outliers  |
| **Correlation & Chemistry Insights**| pandas, seaborn                                         | Quantify feature relationships & domain context  |
| **Dimensionality Reduction**        | PCA (scikit-learn)                                      | Summarize chemistry into interpretable axes      |
| **Clustering**                      | k-Means, silhouette score, elbow method                 | Segment wines by style/process & quality         |
| **Cluster Profiling**               | Groupby, boxplots, countplots                           | Link clusters to quality and chemistry           |
| **Threshold Benchmarking**          | Aggregation (mean/min/max), feature selection           | Set practical targets for wine quality           |
| **Machine Learning Prep**           | StandardScaler, train/test split                        | (Next steps: Classification/Regression models)   |

---

## Key Results & Insights

### 1. **Consumer Scores Are correlated by Chemistry**

- Most wines (both red & white) cluster around “acceptable to good” scores (5–6).
- Features most associated with higher quality:
  - **Red Wine**: High Alcohol, High Sulphates, Low Volatile Acidity, Low Chlorides, High Citric Acid
  - **White Wine**: High Alcohol, High pH, Low Density, Low Chlorides, Low Total Sulfur Dioxide

### 2. **Principal Component Analysis (PCA) Highlights Two Main Quality Axes**

- **PC1**: Grape Ripeness & Fermentation Efficiency
  - High Alcohol, Low Density, High Citric Acid, High Sulphates, Low Volatile Acidity
- **PC2**: Processing/Stabilization
  - High Sulfur Dioxide, More Residual Sugar, Higher Density

**Interpretation**:  
Wines with riper grapes and cleaner fermentation (high PC1, low PC2) consistently receive higher quality scores.

### 3. **Clustering Reveals Quality Benchmarks**

- **Red Wine Cluster #0**  
  - **Highest mean score:** 5.95  
  - **Benchmarks:** Alcohol > 10.6%, Sulphates > 0.75 g/L, VA < 0.41 g/L, Chlorides < 0.10 g/L
- **White Wine Cluster #0**  
  - **Highest mean score:** 6.17  
  - **Benchmarks:** Alcohol > 11.2%, Sulphates > 0.51 g/L, VA < 0.28 g/L, Chlorides < 0.04 g/L

### 4. **Actionable Chemical Targets for Winemaking**

| Variable               | Red Wine Benchmark   | White Wine Benchmark  |
|------------------------|---------------------|----------------------|
| Alcohol (%)            | > 10.6              | > 11.2               |
| Sulphates (g/L)        | > 0.75              | > 0.51               |
| Citric Acid (g/L)      | > 0.48              | > 0.28               |
| Volatile Acidity (g/L) | < 0.41              | < 0.28               |
| Chlorides (g/L)        | < 0.10              | < 0.04               |
| pH                     | > 3.18              | > 3.31               |
| Density                | < 0.9978            | < 0.9920             |
| Total SO₂ (mg/L)       | < 30                | < 123                |
| Residual Sugar (g/L)   | < 2.6               | < 3.4                |

---

## 📦 Repository Structure

```

wine-quality-analysis/
│
├── Wine_Quality_Analysis.ipynb     # Main Jupyter notebook with full workflow
├── winequality-red.csv             # Red wine dataset
├── winequality-white.csv           # White wine dataset
├── wine_combined.csv               # Cleaned and labeled dataset (for dashboard)
├── images/                         # Sample plots and results
│   ├── correlation_heatmap_sample.png
│   ├── red_wine_clusters.png
│   └── ...
└── README.md                       # 📖 This documentation
```

---

## 🚀 How to Run This Notebook

1. **Clone this repository**
2. **Install Python dependencies:**  
   - pandas, numpy, matplotlib, seaborn, scikit-learn, [Jupyter Notebook](https://jupyter.org/)
3. **Download datasets** from UCI if not present.
4. **Run `Wine_Quality_Analysis.ipynb`** step by step to reproduce the full analysis.

---

## 💡 Why This Matters

- **Wine quality** influences commercial pricing, branding, and consumer preference.
- **Objective chemistry** allows scalable, data-driven quality control.
- **Actionable targets** empower winemakers to optimize product characteristics before sensory evaluation.
- **Techniques applied here** extend to other beverages, foods, and industrial quality analytics.

---

## 📜 References

- [Wine Quality Data Set (UCI)](https://archive.ics.uci.edu/dataset/186/wine+quality)
- Cortez, P., Cerdeira, A., Almeida, F., Matos, T., & Reis, J. (2009). Wine Quality Data Set. _UCI Machine Learning Repository_.

---

## 👨‍💻 Author

Data science notebook and documentation by **Renato Silva**

---

**Cheers to Data-Driven Wine!** 🍇🍷

---

> _“The discovery of a good wine is increasingly better for mankind than the discovery of a new star.”_  
> — Leonardo da Vinci

---

## 🏆 Summary Table: Key Benchmarks for Wine Quality

| Wine Type  | Alcohol | Sulphates | VA    | Chlorides | Citric Acid | pH   | Density  | SO₂    | Residual Sugar |
|------------|---------|-----------|-------|-----------|-------------|-------|----------|--------|----------------|
| **Red**    | >10.6%  | >0.75 g/L | <0.41 | <0.10     | >0.48 g/L   | >3.18 | <0.9978  | <30 mg | <2.6 g/L       |
| **White**  | >11.2%  | >0.51 g/L | <0.28 | <0.04     | >0.28 g/L   | >3.31 | <0.9920  | <123mg | <3.4 g/L       |

---
