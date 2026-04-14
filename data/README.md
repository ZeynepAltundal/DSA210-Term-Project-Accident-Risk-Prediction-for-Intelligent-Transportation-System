# Data

The US Accidents dataset cannot be uploaded to GitHub due to its large size (653 MB).

## Primary Dataset — US Accidents (Kaggle)

### How to Download
1. Go to: https://www.kaggle.com/datasets/sobhanmoosavi/us-accidents
2. Sign in to Kaggle (free account required)
3. Click **Download** button
4. Extract the zip file → `US_Accidents_March23.csv`
5. Place the CSV file in this `data/` folder before running the notebooks

### Dataset Info
| Property | Value |
|----------|-------|
| Source | Kaggle — sobhanmoosavi/us-accidents |
| Size | ~653 MB (compressed) |
| Records | 7,728,394 |
| Features | 46 columns |
| Period | January 2016 – March 2023 |
| Coverage | 49 US states |
| License | CC-BY-NC-SA 4.0 |
| Sample Used | 500,000 records (random_state=42) |

### Key Features Used
| Feature | Description |
|---------|-------------|
| Severity | Accident severity (1=low, 4=high) |
| Start_Time | Timestamp of accident start |
| Start_Lat, Start_Lng | GPS coordinates |
| Weather_Condition | Weather at time of accident |
| Temperature(F) | Temperature in Fahrenheit |
| Junction, Traffic_Signal | Road infrastructure features |
| State | US state abbreviation |

---

## External Dataset 1 — US Census Bureau (2020)
| Property | Value |
|----------|-------|
| Source | https://api.census.gov/data/2020/dec/pl |
| Data | State-level population counts |
| Usage | Normalize accident counts per 100K population |
| Access | Free, no API key required |

---

## External Dataset 2 — NOAA Climate Normals (1991–2020)
| Property | Value |
|----------|-------|
| Source | https://www.ncei.noaa.gov/access/us-climate-normals/ |
| Data | Monthly precipitation and temperature averages |
| Usage | Compare accident patterns against climate baselines |
| Access | Free, no registration required |
