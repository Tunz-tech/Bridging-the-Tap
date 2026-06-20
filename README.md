# Bridging-the-Tap
 A Data-Driven Assessment of Sustainable Development Goal (SDG) 6 Progress using WHO/UNICEF JMP Data
# 🌍 Global Water Equity: SDG 6 Target Tracker & Predictive Forecasting Model

## 📌 Project Overview
This project evaluates global progress velocity toward the United Nations Sustainable Development Goal 6 (Universal Access to Clean Water by 2030) using tracking datasets from the WHO/UNICEF Joint Monitoring Programme (WASH). 

By engineering a dynamic predictive pipeline in Python, this repository moves past surface-level historical reporting to construct individual chronological baselines and forecast national trajectories for the 2030 deadline.

---

## 📊 Technical Data Dictionary

The master combined dataset (`JMP_2030_Master_Combined_Analytics.csv`) contains 23 core features capturing historical context, machine learning projections, and calculated linear trajectories:

| Feature/Column Name | Data Type | Source/Type | Description |
| :--- | :--- | :--- | :--- |
| `name` / `Country` | Text | Base Attribute | The official geographic entity/territory name. |
| `region` / `Region` | Text | Regional Mapping | Global geographical macro-region categorization (e.g., Sub-Saharan Africa). |
| `coverage_2020` | Decimal | Base Metric | The baseline national percentage (%) of population with basic water access recorded in the year 2020. |
| `annual_change` | Decimal | ML Engine Feature | The calculated annualized progress coefficient mapped by the machine learning forecasting engine. |
| `projected_2030` | Decimal | ML Model Target | **The primary Machine Learning Forecast.** Projections of national water access levels for the year 2030 (Capped at 100%). |
| `2030_status` | Text | Classification | Categorical classification based on the ML forecast boundaries (e.g., Universal Access, Very High Access). |
| `Start_Year` / `End_Year` | Integer | Historical Audit | The custom chronological boundaries isolated for each nation to find valid data points. |
| `Start_Value` / `End_Value` | Decimal | Historical Audit | The exact historical percentage values at the extracted `Start_Year` and `End_Year` points. |
| `Years_Passed` | Integer | Calculated | Total localized time elapsed between historical data captures (`End_Year - Start_Year`). |
| `Annual_Velocity` | Decimal | Engineered | The baseline calculation of average progress speed per year: `(End_Value - Start_Value) / Years_Passed`. |
| `Projected_2030` | Decimal | Baseline Model | **Traditional Velocity Forecast.** The 2030 linear projection calculated purely on baseline progress speeds. |
| `SDG_2030_Gap` | Decimal | Calculated | The remaining target gap percentage points needed to reach the UN mandate of 100% universal access (`100 - Projected_2030`). |
| `SDG_Status` | Text | Classification | Label assigned based on the linear model trajectory (e.g., Stagnating or Regressing, Off Track). |
| `Prediction_Difference` | Decimal | Engineered | **Divergence Metric.** Evaluates variance between the non-linear Machine Learning output and the traditional Linear Baseline (`projected_2030 - Projected_2030`). |
| `Expected_Improvement` | Decimal | Engineered | The projected growth jump expected between the 2020 baseline and the 2030 deadline (`projected_2030 - coverage_2020`). |
| `Likely_Achieve_SDG` | Boolean | Logic Flag | True/False binary flag tracking whether a territory's 2030 forecast crosses the universal threshold ($\ge 99\%$). |
| `Risk_Category` | Text | Strategic Index | High-level threat assessment grouping applied to the 2030 outcomes: `On Track` ($\ge 99\%$), `Near Target` ($\ge 90\%$), `Moderate Risk` ($\ge 75\%$), or `High Risk` ($< 75\%$). |

---

## 🛠️ Core Analytical Insights
* **Model Divergence:** Positive values in `Prediction_Difference` isolate territories where recent infrastructure deployment waves are actively bending progress trajectories upwards, proving non-linear acceleration.
* **The Stagnation Cluster:** Highlights regions showing an `Annual_Velocity` of exactly `0.0`, isolating critical gridlocks where policy implementation has stalled despite high baseline development.
