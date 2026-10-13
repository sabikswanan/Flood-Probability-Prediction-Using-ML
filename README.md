<div align="center">

<img src="assets/banner.svg" alt="Flood Probability Prediction — animated banner" width="100%"/>

<img src="assets/typing.svg" alt="Predicting flood probability from 20 risk factors · KNN wins with R² = 0.778" width="80%"/>

<br/>

<a href="https://colab.research.google.com/github/sabikswanan/Flood-Probability-Prediction-Using-ML/blob/main/Code%20-%20Flood%20Probability%20Prediction%20using%20ML.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open in Colab" height="28"/></a>
<a href="https://www.kaggle.com/datasets/naiyakhalid/flood-prediction-dataset"><img src="https://img.shields.io/badge/Dataset-Kaggle-20BEFF?style=for-the-badge&logo=kaggle&logoColor=white" alt="Kaggle dataset"/></a>
<img src="https://img.shields.io/badge/Python-3-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python"/>
<img src="https://img.shields.io/badge/scikit--learn-ML-F7931E?style=for-the-badge&logo=scikitlearn&logoColor=white" alt="scikit-learn"/>
<img src="https://img.shields.io/badge/pandas-Data-150458?style=for-the-badge&logo=pandas&logoColor=white" alt="pandas"/>
<img src="https://img.shields.io/badge/Jupyter-Notebook-F37626?style=for-the-badge&logo=jupyter&logoColor=white" alt="Jupyter"/>

<br/><br/>

**[Overview](#overview)** &nbsp;·&nbsp;
**[Dataset](#dataset)** &nbsp;·&nbsp;
**[Pipeline](#pipeline)** &nbsp;·&nbsp;
**[Results](#results)** &nbsp;·&nbsp;
**[Insights](#key-insights)** &nbsp;·&nbsp;
**[Run it](#run-it-yourself)** &nbsp;·&nbsp;
**[Author](#author)**

<br/>

<img src="assets/stats.svg" alt="50,000 regions · 20 flood-risk factors · 4 regression models · best R² 0.778" width="100%"/>

</div>

---

## Overview

Floods are among the most destructive natural disasters, and their risk depends on a mix of climate,
land use, infrastructure and governance. This project asks a simple question:

> **Given 20 risk factors for a region, how well can machine learning predict its flood probability?**

It was built for **CSE437 — Data Science** at **BRAC University**. The notebook explores the data,
prepares it, trains **four regression models** and compares them on **R², MAE and RMSE** to find the
best-performing algorithm.

---

## Dataset

| | |
|---|---|
| **Source** | [Flood Prediction Dataset — Kaggle](https://www.kaggle.com/datasets/naiyakhalid/flood-prediction-dataset) |
| **Rows** | 50,000 regions |
| **Features** | 20 integer risk scores |
| **Target** | `FloodProbability` (continuous, 0–1) |
| **Missing values** | None |
| **Duplicate rows** | None |

<details>
<summary><b>Show all 20 risk factors, grouped by theme</b></summary>
<br/>

| Climate & hydrology | Land use | Infrastructure | Governance & society |
|---|---|---|---|
| MonsoonIntensity | Deforestation | DamsQuality | IneffectiveDisasterPreparedness |
| ClimateChange | Urbanization | DrainageSystems | InadequatePlanning |
| Siltation | AgriculturalPractices | DeterioratingInfrastructure | PoliticalFactors |
| Watersheds | Encroachments | RiverManagement | PopulationScore |
| CoastalVulnerability | TopographyDrainage | | |
| Landslides | | | |
| WetlandLoss | | | |

<sub>The grouping is for readability only; the models use all 20 features as they are.</sub>

</details>

---

## Pipeline

```mermaid
flowchart LR
    A[("Kaggle CSV<br/>50,000 × 21")] --> B["Exploration<br/>nulls · duplicates<br/>correlation"]
    B --> C["Train / test split<br/>80% / 20%"]
    C --> D["StandardScaler<br/>fit on train only"]
    D --> E{"4 regressors"}
    E --> F1["SVR"]
    E --> F2["Decision Tree"]
    E --> F3["Random Forest"]
    E --> F4["KNN"]
    F1 & F2 & F3 & F4 --> G["Evaluate<br/>R² · MAE · RMSE"]
    G --> H["Best model<br/>KNN · R² 0.778"]

    classDef data fill:#0b1d3a,stroke:#22d3ee,color:#ffffff
    classDef step fill:#123b6d,stroke:#3b82f6,color:#ffffff
    classDef model fill:#1e293b,stroke:#a78bfa,color:#ffffff
    classDef best fill:#fbbf24,stroke:#b45309,color:#0b1d3a
    class A data
    class B,C,D,G step
    class E,F1,F2,F3,F4 model
    class H best
```

1. **Exploration:** shape, data types, missing values, duplicates, and a full correlation matrix.
2. **Split:** 40,000 rows for training and 10,000 for testing (`random_state = 1`).
3. **Scaling:** `StandardScaler` fitted on the training set only, so no test information leaks in.
4. **Modelling:** Support Vector Regression, Decision Tree, Random Forest and K-Nearest Neighbours.
5. **Evaluation:** R², Mean Absolute Error and Root Mean Squared Error on the held-out test set.

---

## Results

<div align="center">
<img src="assets/leaderboard.svg" alt="Model leaderboard: KNN 0.778, Random Forest 0.732, SVR 0.709, Decision Tree 0.135" width="100%"/>
</div>

<br/>

| Rank | Model | R² ↑ | MAE ↓ | RMSE ↓ |
|:---:|---|:---:|:---:|:---:|
| 🥇 | **K-Nearest Neighbours** | **0.7776** | **0.0186** | **0.0238** |
| 🥈 | Random Forest | 0.7315 | 0.0205 | 0.0261 |
| 🥉 | Support Vector Regression | 0.7090 | 0.0207 | 0.0272 |
| 4 | Decision Tree | 0.1346 | 0.0372 | 0.0469 |

**KNN explains about 78% of the variation in flood probability**, with a typical error of under
two percentage points.

<details>
<summary><b>How does each model work? (one-line explanations)</b></summary>
<br/>

| Model | Idea in one line |
|---|---|
| **KNN** | Predicts a region's flood probability as the average of the 5 most similar regions. |
| **Random Forest** | Averages 100 decision trees, each trained on a random sample of the data. |
| **SVR** | Fits a smooth function that keeps most predictions within a small error margin. |
| **Decision Tree** | Splits the data with yes/no questions until each leaf gives a prediction. |

</details>

---

## What drives flood risk?

<div align="center">
<img src="assets/correlations.svg" alt="Correlation of each of the 20 factors with FloodProbability, all between 0.215 and 0.229" width="100%"/>
</div>

Every factor correlates with flood probability at almost exactly the same strength (r ≈ 0.22), while
the factors are almost uncorrelated with each other. **No single factor dominates.** Flood risk here
builds up from many small contributions, so a model has to look at all 20 together.

---

## Key insights

- **KNN came out on top (R² 0.778).** Regions with similar risk profiles tend to have similar flood
  probabilities, which is exactly what a neighbour-based model exploits.
- **Ensembles beat single trees by a wide margin.** An unrestricted Decision Tree memorises noise in
  the training data (R² 0.135), while averaging 100 trees in a Random Forest lifts R² to 0.732.
- **Predictions lean towards the average.** In the actual-vs-predicted plot, KNN slightly
  overestimates low-risk regions and underestimates high-risk ones, because averaging neighbours pulls
  extreme values towards the middle.
- **The signal is spread evenly.** All 20 features are about equally correlated with the target and
  barely overlap with each other, so the models use every factor as input.

---

## Visual gallery

<details open>
<summary><b>Plots from the notebook (click to collapse)</b></summary>
<br/>

<table>
  <tr>
    <td align="center"><img src="assets/plots/actual-vs-predicted-knn.png" alt="Actual vs predicted flood probability for KNN" width="100%"/><br/><sub><b>Actual vs. predicted (KNN)</b></sub></td>
    <td align="center"><img src="assets/plots/metrics-comparison.png" alt="R², MAE and RMSE for all four models" width="100%"/><br/><sub><b>Metric comparison</b></sub></td>
  </tr>
  <tr>
    <td align="center"><img src="assets/plots/model-r2.png" alt="R² score per model" width="100%"/><br/><sub><b>R² per model</b></sub></td>
    <td align="center"><img src="assets/plots/feature-correlation.png" alt="Correlation of each feature with FloodProbability" width="100%"/><br/><sub><b>Feature correlation with target</b></sub></td>
  </tr>
  <tr>
    <td colspan="2" align="center"><img src="assets/plots/correlation-heatmap.png" alt="Correlation heatmap of all features" width="60%"/><br/><sub><b>Correlation heatmap — features are nearly independent of one another</b></sub></td>
  </tr>
</table>

</details>

---

## Run it yourself

### Option 1 — Google Colab (no setup)

<a href="https://colab.research.google.com/github/sabikswanan/Flood-Probability-Prediction-Using-ML/blob/main/Code%20-%20Flood%20Probability%20Prediction%20using%20ML.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open in Colab" height="28"/></a>

1. Click the badge above to open the notebook.
2. Download the CSV from [Kaggle](https://www.kaggle.com/datasets/naiyakhalid/flood-prediction-dataset).
3. Upload it to Colab's file panel and name it `Dataset - Flood Prediction.csv`.
4. Choose **Runtime → Run all**.

### Option 2 — Run locally

```bash
git clone https://github.com/sabikswanan/Flood-Probability-Prediction-Using-ML.git
cd Flood-Probability-Prediction-Using-ML
pip install pandas numpy scikit-learn matplotlib seaborn jupyter
jupyter notebook
```

<details>
<summary><b>Running locally? Change one line first</b></summary>
<br/>

The notebook reads the dataset from Colab's `/content/` folder. Put the CSV next to the notebook
and update the path in the first data cell:

```python
df = pd.read_csv("Dataset - Flood Prediction.csv")
```

</details>

---

## Project structure

```text
Flood-Probability-Prediction-Using-ML/
├── Code - Flood Probability Prediction using ML.ipynb   # full analysis and models
├── README.md
└── assets/
    ├── *.svg          # animated graphics used in this README
    └── plots/         # figures exported from the notebook
```

---

## Future work

- [ ] Try **Linear and Ridge Regression**, since every feature contributes almost equally to the target
- [ ] Tune hyperparameters (number of neighbours for KNN, tree depth, SVR kernel) with **k-fold cross-validation**
- [ ] Add **gradient boosting** models such as XGBoost
- [ ] Explain individual predictions with **SHAP values**
- [ ] Deploy a small web app where users enter risk scores and get a flood probability

---

## Author

<div align="center">

**Sabik Swanan**<br/>
B.Sc. in Computer Science · BRAC University<br/>
<sub>CSE437 — Data Science</sub>

<br/>

<a href="https://github.com/sabikswanan"><img src="https://img.shields.io/badge/GitHub-sabikswanan-181717?style=for-the-badge&logo=github&logoColor=white" alt="GitHub"/></a>
<a href="https://www.linkedin.com/in/sabikswanan"><img src="https://img.shields.io/badge/LinkedIn-sabikswanan-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn"/></a>
<a href="mailto:sabikswanan@gmail.com"><img src="https://img.shields.io/badge/Email-sabikswanan@gmail.com-EA4335?style=for-the-badge&logo=gmail&logoColor=white" alt="Email"/></a>

<br/><br/>

<sub>If this project helped you, consider giving it a ⭐</sub>

<img src="assets/footer.svg" alt="" width="100%"/>

</div>
