# Accident Risk Prediction for Intelligent Transportation Systems

**DSA 210 — Spring 2025–2026**

**Sabancı University**

**Student ID: Zeynep Altundal 31978**

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

## Planned Analysis

### Stage 1 — Data Collection & Preprocessing
- Download and sample the US Accidents dataset (500K from 7.7M)
- Parse timestamps and engineer temporal features (Hour, DayOfWeek, Month, TimeOfDay, IsWeekend)
- Map 100+ raw weather strings to 8 broad categories
- Handle missing values and remove physically impossible readings

### Stage 2 — Exploratory Data Analysis
- Accident distribution across time (hour, day, month, year)
- Weather conditions vs. severity patterns
- Geographic distribution across US states using GPS coordinates
- Road infrastructure features (junctions, traffic signals) vs. high-risk rates
- External enrichment: accidents per 100K population (Census), climate baseline comparisons (NOAA)

### Stage 3 — Hypothesis Testing
- H1: Weekday severity vs. weekend severity — Mann-Whitney U Test
- H2: Weather category effect on severity — Kruskal-Wallis Test
- H3: Time of day effect on high-risk rate — Chi-Square Test
- H4: Rush hour accident proportion — One-sample Z-Test (Proportion)

### Stage 4 — Predictive Modeling *(upcoming)*
- Logistic Regression baseline
- Random Forest classifier
- Evaluation: Accuracy, F1-score, Precision, Recall, ROC-AUC

---

## Tools

- **Python** — all analysis and modeling
- **Pandas, NumPy** — data manipulation
- **Matplotlib, Seaborn** — visualization
- **SciPy, Statsmodels** — hypothesis testing
- **Scikit-learn** — machine learning models *(Phase 3)*
- **Google Colab** — development environment

---

## Notes on Data Limitations & AI Usage

- The US Accidents dataset relies on traffic impact data from two APIs (MapQuest and Bing Maps) and may underrepresent accidents in rural or low-coverage areas.

- The dataset does not include accidents where no traffic impact was recorded; this may introduce a bias toward higher-severity events in certain regions.

- A random sample of 500,000 records was used for computational feasibility. While statistically representative, some rare weather conditions or geographic regions may be underrepresented.

- Population data (US Census 2020) and climate normals (NOAA 1991–2020) reflect historical baselines and do not capture recent demographic or climate shifts.

- AI tools including Claude (Anthropic) were used for guidance in code development, debugging, and refining analysis explanations throughout the project.



