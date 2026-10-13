<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0052D4,50:4364F7,100:6FB1FC&height=260&section=header&text=Flood%20Probability%20Prediction&fontSize=48&fontColor=FFFFFF&fontAlignY=38&animation=fadeIn&desc=Machine%20Learning%20%E2%80%A2%2050%2C000%20regions%20%E2%80%A2%2020%20risk%20factors%20%E2%80%A2%204%20models&descSize=17&descAlignY=58&descAlign=50" alt="Flood Probability Prediction" width="100%"/>

<a href="https://github.com/sabikswanan/Flood-Probability-Prediction-Using-ML"><img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=600&size=21&duration=3000&pause=1000&color=36BCF7&center=true&vCenter=true&width=780&lines=%3E+Predicting+flood+probability+from+20+risk+factors;%3E+Benchmarking+SVR%2C+Decision+Tree%2C+Random+Forest+%26+KNN;%3E+Best+model%3A+KNN+%7C+R%C2%B2+%3D+0.778+%7C+RMSE+%3D+0.024" alt="Predicting flood probability from 20 risk factors · Best model KNN, R² 0.778"/></a>

<br/>

<img src="https://img.shields.io/badge/REGIONS-50%2C000-0052D4?style=for-the-badge&labelColor=0B1220" alt="50,000 regions"/>
<img src="https://img.shields.io/badge/RISK%20FACTORS-20-4364F7?style=for-the-badge&labelColor=0B1220" alt="20 risk factors"/>
<img src="https://img.shields.io/badge/MODELS-4-1E90FF?style=for-the-badge&labelColor=0B1220" alt="4 models"/>
<img src="https://img.shields.io/badge/BEST%20R%C2%B2-0.778%20%C2%B7%20KNN-00B4DB?style=for-the-badge&labelColor=0B1220" alt="Best R² 0.778 with KNN"/>

<a href="https://colab.research.google.com/github/sabikswanan/Flood-Probability-Prediction-Using-ML/blob/main/Code%20-%20Flood%20Probability%20Prediction%20using%20ML.ipynb"><img src="https://img.shields.io/badge/Open%20in-Colab-F9AB00?style=for-the-badge&logo=googlecolab&logoColor=white&labelColor=0B1220" alt="Open in Colab"/></a>
<a href="https://www.kaggle.com/datasets/naiyakhalid/flood-prediction-dataset"><img src="https://img.shields.io/badge/Dataset-Kaggle-20BEFF?style=for-the-badge&logo=kaggle&logoColor=white&labelColor=0B1220" alt="Kaggle dataset"/></a>
<img src="https://img.shields.io/badge/Python-3-3776AB?style=for-the-badge&logo=python&logoColor=white&labelColor=0B1220" alt="Python"/>
<img src="https://img.shields.io/badge/scikit--learn-ML-0083B0?style=for-the-badge&logo=scikitlearn&logoColor=white&labelColor=0B1220" alt="scikit-learn"/>
<img src="https://img.shields.io/badge/pandas-NumPy-150458?style=for-the-badge&logo=pandas&logoColor=white&labelColor=0B1220" alt="pandas and NumPy"/>

<br/><br/>

**[Overview](#overview)** &nbsp;|&nbsp;
**[Dataset](#dataset)** &nbsp;|&nbsp;
**[Pipeline](#pipeline)** &nbsp;|&nbsp;
**[Results](#results)** &nbsp;|&nbsp;
**[Insights](#insights)** &nbsp;|&nbsp;
**[Getting Started](#getting-started)** &nbsp;|&nbsp;
**[Author](#author)**

</div>

<br/>

<a name="overview"></a>

## 🌊 Overview

Floods are among the most destructive natural disasters, and their risk depends on a combination of
climate, land use, infrastructure and governance factors. This project answers one question:

> [!NOTE]
> **Given 20 risk factors for a region, how accurately can machine learning predict its flood probability?**

Built for **CSE437 — Data Science** at **BRAC University**, the notebook covers the full workflow:
exploratory analysis, preprocessing, training **four regression models**, and benchmarking them on
**R², MAE and RMSE** to select the best-performing algorithm.

<br/>

<a name="dataset"></a>

## 📦 Dataset

| Property | Value |
|---|---|
| **Source** | [Flood Prediction Dataset — Kaggle](https://www.kaggle.com/datasets/naiyakhalid/flood-prediction-dataset) |
| **Rows** | 50,000 regions |
| **Features** | 20 integer risk scores |
| **Target** | `FloodProbability` (continuous, 0–1) |
| **Missing values** | None |
| **Duplicate rows** | None |

<details>
<summary><b>View all 20 risk factors, grouped by domain</b></summary>
<br/>

| Climate & Hydrology | Land Use | Infrastructure | Governance & Society |
|---|---|---|---|
| MonsoonIntensity | Deforestation | DamsQuality | IneffectiveDisasterPreparedness |
| ClimateChange | Urbanization | DrainageSystems | InadequatePlanning |
| Siltation | AgriculturalPractices | DeterioratingInfrastructure | PoliticalFactors |
| Watersheds | Encroachments | RiverManagement | PopulationScore |
| CoastalVulnerability | TopographyDrainage | | |
| Landslides | | | |
| WetlandLoss | | | |

<sub>Grouping is for readability only; all 20 features are used as model inputs.</sub>

</details>

<br/>

<a name="pipeline"></a>

## ⚙️ Pipeline

```mermaid
flowchart LR
    A[("Kaggle CSV<br/>50,000 × 21")] --> B(["Exploratory<br/>Analysis"])
    B --> C(["Train / Test Split<br/>80 : 20"])
    C --> D(["StandardScaler<br/>fit on train only"])
    D --> E{{"Model<br/>Benchmark"}}
    E --> F1(["SVR"])
    E --> F2(["Decision Tree"])
    E --> F3(["Random Forest"])
    E --> F4(["KNN"])
    F1 & F2 & F3 & F4 --> G(["Evaluation<br/>R² · MAE · RMSE"])
    G --> H(["🏆 KNN<br/>R² 0.778"])

    classDef data fill:#0B1220,stroke:#36BCF7,stroke-width:2px,color:#E6F4FF
    classDef s1 fill:#0052D4,stroke:#0052D4,color:#FFFFFF
    classDef s2 fill:#4364F7,stroke:#4364F7,color:#FFFFFF
    classDef bench fill:#1E90FF,stroke:#1E90FF,color:#FFFFFF
    classDef model fill:#E6F4FF,stroke:#6FB1FC,stroke-width:1.5px,color:#0B1220
    classDef eval fill:#0083B0,stroke:#0083B0,color:#FFFFFF
    classDef best fill:#00D2FF,stroke:#0052D4,stroke-width:2px,color:#0B1220
    class A data
    class B,C s1
    class D s2
    class E bench
    class F1,F2,F3,F4 model
    class G eval
    class H best
    linkStyle default stroke:#36BCF7,stroke-width:2px
```

| Stage | Details |
|---|---|
| **Exploratory analysis** | Shape, data types, missing values, duplicates and a full correlation matrix |
| **Split** | 40,000 training rows and 10,000 test rows (`random_state = 1`) |
| **Scaling** | `StandardScaler` fitted on the training set only to prevent data leakage |
| **Modelling** | Support Vector Regression, Decision Tree, Random Forest, K-Nearest Neighbours |
| **Evaluation** | R², Mean Absolute Error and Root Mean Squared Error on the held-out test set |

<br/>

<a name="results"></a>

## 🏆 Results

```mermaid
%%{init: {"themeVariables": {"xyChart": {"plotColorPalette": "#1E90FF", "titleColor": "#0083B0"}}}}%%
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

> [!TIP]
> **KNN explains ~78% of the variance in flood probability**, with a mean absolute error of under
> two percentage points on 10,000 unseen regions.

<details>
<summary><b>How each model works</b></summary>
<br/>

| Model | Approach |
|---|---|
| **K-Nearest Neighbours** | Predicts a region's flood probability as the average of its 5 most similar regions. |
| **Random Forest** | Averages 100 decision trees, each trained on a bootstrap sample of the data. |
| **Support Vector Regression** | Fits a smooth function that keeps most predictions within a small error margin. |
| **Decision Tree** | Recursively splits the data on feature thresholds until each leaf yields a prediction. |

</details>

### 📈 Feature correlation with the target

```mermaid
%%{init: {"xyChart": {"height": 620}, "themeVariables": {"xyChart": {"plotColorPalette": "#00B4DB", "titleColor": "#0083B0"}}}}%%
xychart-beta horizontal
    title "Pearson correlation with FloodProbability"
    x-axis ["Infrastructure", "Topography", "River mgmt", "Watersheds", "Dams", "Population", "Siltation", "Preparedness", "Political", "Monsoon", "Wetland loss", "Planning", "Landslides", "Agriculture", "Climate", "Urbanization", "Deforestation", "Encroachment", "Drainage", "Coastal"]
    y-axis "Pearson r" 0 --> 0.25
    bar [0.229, 0.229, 0.229, 0.228, 0.227, 0.227, 0.227, 0.225, 0.225, 0.224, 0.224, 0.223, 0.223, 0.222, 0.221, 0.221, 0.220, 0.218, 0.218, 0.215]
```

All 20 factors correlate with flood probability at nearly identical strength (r ≈ 0.22), while being
almost uncorrelated with one another. **No single factor dominates** — risk accumulates from many
small contributions, so the model must consider all 20 together.

<br/>

<a name="insights"></a>

## 💡 Key Insights

<table>
  <tr>
    <td width="50%" valign="top">
      <h4>🎯 KNN performs best</h4>
      R² <b>0.778</b>. Regions with similar risk profiles have similar flood probabilities, which a
      neighbour-based model exploits directly.
    </td>
    <td width="50%" valign="top">
      <h4>🌲 Ensembles beat single trees</h4>
      An unrestricted Decision Tree overfits (R² <b>0.135</b>); averaging 100 trees in a Random
      Forest raises R² to <b>0.732</b>.
    </td>
  </tr>
  <tr>
    <td width="50%" valign="top">
      <h4>📉 Predictions regress to the mean</h4>
      KNN slightly overestimates low-risk regions and underestimates high-risk ones, as neighbour
      averaging pulls extremes toward the centre.
    </td>
    <td width="50%" valign="top">
      <h4>🧩 Signal is evenly distributed</h4>
      Every feature is roughly equally correlated with the target and largely independent of the
      others, so all 20 are kept as inputs.
    </td>
  </tr>
</table>

> [!NOTE]
> Full visualisations — correlation heatmap, actual-vs-predicted scatter and metric comparisons — are
> available in the [notebook](Code%20-%20Flood%20Probability%20Prediction%20using%20ML.ipynb).

<br/>

<a name="getting-started"></a>

## 🚀 Getting Started

**Option 1 — Google Colab (no setup)**

1. Open the notebook with the **Open in Colab** badge at the top.
2. Download the CSV from [Kaggle](https://www.kaggle.com/datasets/naiyakhalid/flood-prediction-dataset).
3. Upload it to Colab's file panel as `Dataset - Flood Prediction.csv`.
4. Select **Runtime → Run all**.

**Option 2 — Local environment**

```bash
git clone https://github.com/sabikswanan/Flood-Probability-Prediction-Using-ML.git
cd Flood-Probability-Prediction-Using-ML
pip install pandas numpy scikit-learn matplotlib seaborn jupyter
jupyter notebook
```

<details>
<summary><b>Note for local runs</b></summary>
<br/>

The notebook reads the dataset from Colab's `/content/` directory. Place the CSV next to the notebook
and update the path in the first data cell:

```python
df = pd.read_csv("Dataset - Flood Prediction.csv")
```

</details>

<br/>

## 🗺️ Roadmap

- [ ] Benchmark **Linear and Ridge Regression**, given the near-additive structure of the features
- [ ] Hyperparameter tuning (k for KNN, tree depth, SVR kernel) with **k-fold cross-validation**
- [ ] Add **gradient boosting** models such as XGBoost
- [ ] Model explainability with **SHAP**
- [ ] Deploy as a lightweight web service for interactive flood-risk scoring

<br/>

<a name="author"></a>

## 👤 Author

<div align="center">

### Sabik Swanan

B.Sc. in Computer Science · BRAC University

<br/>

<a href="https://github.com/sabikswanan"><img src="https://img.shields.io/badge/GitHub-sabikswanan-0052D4?style=for-the-badge&logo=github&logoColor=white&labelColor=0B1220" alt="GitHub"/></a>
<a href="https://www.linkedin.com/in/sabikswanan"><img src="https://img.shields.io/badge/LinkedIn-sabikswanan-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white&labelColor=0B1220" alt="LinkedIn"/></a>
<a href="https://mail.google.com/mail/?view=cm&fs=1&to=sabikswanan@gmail.com"><img src="https://img.shields.io/badge/Email-sabikswanan%40gmail.com-00B4DB?style=for-the-badge&logo=gmail&logoColor=white&labelColor=0B1220" alt="Email"/></a>

<br/><br/>

<sub>⭐ Star this repo if you found it useful</sub>

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:6FB1FC,50:4364F7,100:0052D4&height=130&section=footer" alt="" width="100%"/>

</div>
