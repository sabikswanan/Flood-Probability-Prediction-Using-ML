<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0b1d3a,50:123b6d,100:22d3ee&height=230&section=header&text=Flood%20Probability%20Prediction&fontSize=46&fontColor=ffffff&fontAlignY=36&animation=fadeIn&desc=Machine-learning%20regression%20on%2050%2C000%20regions%20and%2020%20flood-risk%20factors&descSize=17&descAlignY=56&descAlign=50" alt="Flood Probability Prediction" width="100%"/>

<a href="https://github.com/sabikswanan/Flood-Probability-Prediction-Using-ML"><img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=600&size=22&duration=3200&pause=900&color=22D3EE&center=true&vCenter=true&width=760&lines=Predicting+flood+probability+from+20+risk+factors;Training+SVR%2C+Decision+Tree%2C+Random+Forest+%26+KNN;KNN+wins%3A+R%C2%B2+%3D+0.778%2C+RMSE+%3D+0.024" alt="Predicting flood probability from 20 risk factors · KNN wins with R² = 0.778"/></a>

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

<table>
  <tr>
    <td align="center" width="25%"><h2>50,000</h2><sub>regions in the dataset</sub></td>
    <td align="center" width="25%"><h2>20</h2><sub>flood-risk factors</sub></td>
    <td align="center" width="25%"><h2>4</h2><sub>regression models</sub></td>
    <td align="center" width="25%"><h2>0.778</h2><sub>best R² (KNN)</sub></td>
  </tr>
</table>

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

```mermaid
%%{init: {"themeVariables": {"xyChart": {"plotColorPalette": "#fbbf24"}}}}%%
xychart-beta
    title "Test-set R² by model (higher is better)"
    x-axis ["KNN", "Random Forest", "SVR", "Decision Tree"]
    y-axis "R² score" 0 --> 1
    bar [0.778, 0.732, 0.709, 0.135]
```

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

```mermaid
%%{init: {"xyChart": {"height": 620}, "themeVariables": {"xyChart": {"plotColorPalette": "#22d3ee"}}}}%%
xychart-beta horizontal
    title "Correlation of each factor with FloodProbability"
    x-axis ["Infrastructure", "Topography", "River mgmt", "Watersheds", "Dams", "Population", "Siltation", "Preparedness", "Political", "Monsoon", "Wetland loss", "Planning", "Landslides", "Agriculture", "Climate", "Urbanization", "Deforestation", "Encroachment", "Drainage", "Coastal"]
    y-axis "Pearson r" 0 --> 0.25
    bar [0.229, 0.229, 0.229, 0.228, 0.227, 0.227, 0.227, 0.225, 0.225, 0.224, 0.224, 0.223, 0.223, 0.222, 0.221, 0.221, 0.220, 0.218, 0.218, 0.215]
```

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

> 📊 The full set of plots (correlation heatmap, actual-vs-predicted scatter and metric comparisons)
> is in the [notebook](Code%20-%20Flood%20Probability%20Prediction%20using%20ML.ipynb).

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

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:22d3ee,50:123b6d,100:0b1d3a&height=120&section=footer" alt="" width="100%"/>

</div>
