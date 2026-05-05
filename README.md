# Accident Risk Prediction for Intelligent Transportation Systems

**DSA 210 — Spring 2025–2026**
**Sabancı University**
**Student: Zeynep Altundal | 31978**

---

## Motivation

Traffic accidents remain one of the leading causes of injury and loss of life worldwide, posing a significant challenge for modern transportation systems. With the rapid advancement of autonomous driving technologies and intelligent transportation systems, understanding the underlying factors that contribute to accident occurrence has become increasingly critical.

As a student with a strong interest in robotics and autonomous systems, I am particularly motivated to explore how data-driven approaches can enhance safety in real-world environments. Autonomous vehicles rely heavily on perception, decision-making, and risk assessment modules, all of which depend on accurately understanding environmental and temporal conditions.

This project analyzes large-scale real-world traffic accident data to develop predictive models for accident risk. By identifying key contributing factors such as weather conditions, time of day, and road characteristics, it aims to support safer decision-making in intelligent transportation systems.

---

## Data Sources

| Source | Description | Role |
|--------|-------------|------|
| [US Accidents — Kaggle](https://www.kaggle.com/datasets/sobhanmoosavi/us-accidents) | 7,728,394 records (Jan 2016 – Mar 2023): severity, GPS coordinates, weather conditions, road features | Primary |
| [US Census Bureau 2020](https://api.census.gov/data/2020/dec/pl) | State-level population counts for all 50 states | Enrichment |
| [NOAA Climate Normals 1991–2020](https://www.ncei.noaa.gov/access/us-climate-normals/) | Monthly US precipitation and temperature averages | Enrichment |

---

## Project Structure

```
├── notebooks/
│   ├── 0_full_analysis.ipynb              # Phase 2: EDA + Hypothesis Testing
│   ├── 4_external_data_enrichment.ipynb   # Phase 2: Census + NOAA enrichment
│   ├── 5a_data_prep_for_ml.ipynb          # Phase 4: Data preparation for ML
│   ├── 5b_model_training.ipynb            # Phase 4: Model training & evaluation
│   └── 5c_model_analysis.ipynb            # Phase 4: Model analysis & interpretation
├── figures/
│   ├── eda/                               # EDA visualizations
│   ├── enrichment/                        # External enrichment visualizations
│   ├── hypothesis/                        # Hypothesis test visualizations
│   └── ml/                               # Machine learning visualizations
├── data/
├── requirements.txt
└── README.md
```

---

## Analysis Pipeline

### Stage 1 — Data Collection & Preprocessing
- Download and sample the US Accidents dataset (500K from 7.7M records)
- Parse timestamps and engineer temporal features (Hour, DayOfWeek, Month, TimeOfDay, IsWeekend)
- Map 100+ raw weather strings to 8 broad categories
- Handle missing values and remove physically impossible readings
- Enrich with US Census population data and NOAA Climate Normals

### Stage 2 — Exploratory Data Analysis
- Accident distribution across time (hour, day, month, year)
- Weather conditions vs. severity patterns
- Geographic distribution across US states using GPS coordinates
- Road infrastructure features (junctions, traffic signals) vs. high-risk rates
- External enrichment: accidents per 100K population (Census), climate baseline comparisons (NOAA)

### Stage 3 — Hypothesis Testing

| # | Hypothesis | Method | Result |
|---|-----------|--------|--------|
| H1 | Weekday severity vs. weekend severity | Mann-Whitney U Test | Fail to Reject H₀ |
| H2 | Weather category effect on severity | Kruskal-Wallis Test | Reject H₀ ✓ |
| H3 | Time of day effect on high-risk rate | Chi-Square Test | Reject H₀ ✓ |
| H4 | Rush hour accident proportion | One-sample Z-Test | Reject H₀ ✓ |

Key findings:
- **Snow and Rain** conditions produce significantly higher accident severity than Clear weather
- **Evening hours (17:00–21:00)** have the highest high-risk rate at 22.8%
- **Rush hours** account for 32.7% of all accidents vs expected 20.8%

### Stage 4 — Machine Learning

**Target variable:** `HighRisk` — binary label (Severity ≥ 3 → 1, else → 0)

**Features used:**
- Temporal: Hour, Month, IsWeekend, IsRushHour, TimeOfDay
- Weather: Temperature, Visibility, Humidity, Pressure, Wind Speed, WeatherCategory
- Road infrastructure: Junction, Traffic Signal, Crossing, and 5 others
- Census enrichment: accidents_per_100k (state-level population normalization)
- NOAA enrichment: Normal_Precip_in, Normal_Temp_F, Above_Normal_Precip

**Models trained:**

| Model | Type | Lecture Reference |
|-------|------|-------------------|
| Logistic Regression | Linear baseline | Week 9 — gradient descent |
| Random Forest | Ensemble — Bagging | Week 10 — bagging + random feature subsets |
| Gradient Boosting | Ensemble — Boosting | Week 10 — sequential weak learners |

**Evaluation strategy:**
- Stratified 80/20 train/test split
- 5-fold stratified cross-validation
- Metrics: Accuracy, Precision, Recall, F1-score, ROC-AUC
- Majority class baseline comparison

---

## Key Results

### Hypothesis Testing
- 3 out of 4 hypotheses confirmed
- Adverse weather, evening hours, and rush hours are statistically confirmed risk factors

### Machine Learning
- Ensemble models (Random Forest, Gradient Boosting) outperform Logistic Regression baseline
- Most predictive features: Hour, Visibility, Junction, IsRushHour, Temperature
- Census and NOAA enrichment features add meaningful state-level and seasonal context
- Cross-validation confirms model stability across different data splits

---

## Tools & Libraries

| Tool | Purpose |
|------|---------|
| Python | All analysis and modeling |
| Pandas, NumPy | Data manipulation |
| Matplotlib, Seaborn | Visualization |
| SciPy, Statsmodels | Hypothesis testing |
| Scikit-learn | Machine learning models |
| Requests | Census and NOAA API calls |
| Google Colab | Development environment |

---

## How to Reproduce

1. Clone this repository
2. Install dependencies:
```bash
pip install -r requirements.txt
```
3. Run notebooks in order:
```
notebooks/0_full_analysis.ipynb
notebooks/4_external_data_enrichment.ipynb
notebooks/5a_data_prep_for_ml.ipynb
notebooks/5b_model_training.ipynb
notebooks/5c_model_analysis.ipynb
```
4. Each notebook downloads the dataset automatically via the Kaggle API.
   Add your own Kaggle credentials in the download cell.

---

## Limitations & Future Work

**Limitations:**
- The US Accidents dataset relies on traffic impact APIs and may underrepresent rural accidents
- Dataset does not include accidents where no traffic impact was recorded — bias toward higher severity
- A random sample of 500K records was used for computational feasibility
- Census (2020) and NOAA (1991–2020) data reflect historical baselines

**Future Work:**
- Hyperparameter tuning with GridSearchCV / RandomizedSearchCV
- Geospatial clustering features — accident hotspot zones from GPS coordinates
- Real-time traffic density integration
- Deploy as REST API for real-time risk scoring in ITS applications

---

## AI Disclosure

AI tools including Claude (Anthropic), ChatGpt were used for guidance in code development, debugging. All prompts and outputs were reviewed and integrated by the student.



