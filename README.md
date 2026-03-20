# 🧠 HR Attrition Prediction & Workforce Risk Analysis
---

## 📌 Overview

Employee attrition is costly. Organizations often react *after* employees resign, losing valuable talent and incurring high recruitment and onboarding costs. This project uses machine learning to **proactively identify at-risk employees** and equip HR teams with clear, data-driven insights for strategic retention planning.

---

## 🎯 Objectives

- Identify the **key drivers** of employee attrition through EDA
- Build and compare **5 classification models** to predict resignation probability
- Apply **feature selection** using Random Forest importance and the Elbow Method
- Explain predictions using **SHAP value analysis** (XGBoost TreeExplainer)
- Visualize workforce risk patterns via an **interactive Power BI dashboard**
- Deliver **actionable HR recommendations** to reduce attrition

---

## 📂 Repository Structure

```
├── hr_attrition.ipynb                         # Main notebook — EDA, ML models, SHAP
├── HR-Employee-Attrition (1).csv              # IBM HR dataset (1470 records)
├── HR_attrition_report.pdf                    # final report
├── HR_attrition_detailed_summary (1).pdf      # Full attrition analysis summary
├── shap_analysis.pdf                          # SHAP explainability plots (3 plot types)
├── HR_dashboard_1.pbix                        # Power BI dashboard raw file
├── PowerBI_Dashboard_Hr_attrition_proj....png # Power BI dashboard pdf
├── insights_hr_attrition.png                  # EDA insights visualization
├── ml_analysis_result_hr_attrition.png        # Model comparison results
├── top_influential_features.png               # Random Forest feature importance chart
└── README.md
```

---

## 📊 Dataset

| Property | Details |
|---|---|
| Source | IBM HR Employee Attrition Dataset |
| Records | 1,470 employees |
| Features | 35 HR-related attributes |
| Attrition Rate | 16.12% (imbalanced — handled via stratified split + class weighting) |

**Feature categories:**
- Demographics — Age, Gender, Marital Status
- Job details — Role, Department, Job Level, Years at Company
- Compensation — Monthly Income, Daily Rate, Hourly Rate, Salary Hike %, Stock Option Level
- Satisfaction scores — Job, Environment, Relationship, Work-Life Balance
- Work patterns — Overtime, Distance from Home, Business Travel frequency

---

## 🔧 Data Preprocessing

**Outlier Removal — IQR Method (per column):**
Individual IQR-based filtering was applied to 15+ numerical columns including Age, DailyRate, DistanceFromHome, EmployeeNumber, EnvironmentSatisfaction, HourlyRate, RelationshipSatisfaction, StockOptionLevel, TotalWorkingYears, TrainingTimesLastYear, WorkLifeBalance, YearsAtCompany, YearsInCurrentRole, YearsSinceLastPromotion, and YearsWithCurrManager.

**Additional steps:**
- Verified zero missing values across all columns
- Encoded categorical variables using OneHotEncoding and Label Encoding
- Scaled numerical features using StandardScaler inside sklearn Pipelines
- Applied **stratified train-test splitting** at 20%, 30%, and 40% splits to test model stability

---

## 📈 Exploratory Data Analysis

Key findings from histograms, boxplots, and a full correlation heatmap:

| Insight | Finding |
|---|---|
| 🕐 Overtime | Employees working overtime are the highest attrition risk group |
| 💰 Income | Lower monthly income strongly correlates with resignation |
| 📅 Tenure | Employees with fewer than 5 years at the company leave more |
| 🚗 Commute | Longer distance from home negatively impacts retention |
| 😞 Satisfaction | Low job and environment satisfaction are strong attrition signals |
| 🏢 Department | Sales roles show the highest attrition rates |
| 📈 Stock Options | Employees with no stock options are significantly more likely to leave |

---

## 🤖 Machine Learning Models

Five classifiers were trained and evaluated across three train-test split ratios (20% / 30% / 40%):

| Model | Configuration | Notes |
|---|---|---|
| Logistic Regression | max_iter=500 | Baseline model |
| Random Forest | 300 estimators, class_weight=balanced | Used for feature importance extraction |
| XGBoost | lr=0.05, max_depth=6, subsample=0.8 | Used for SHAP analysis |
| CatBoost | 300 iterations, lr=0.05 | Handles categoricals natively |
| **SVM** ✅ | **RBF kernel, class_weight=balanced** | **Final best model** |

**Evaluation metrics:** Accuracy · Precision · Recall · F1-Score · ROC-AUC

**Model comparison methods:**
- ROC Curve overlay for all 5 models at each split
- F1 Score bar chart comparison across all 3 splits

---

## 🔍 Feature Selection — Random Forest + Elbow Method

1. Trained Random Forest (300 estimators) to extract feature importances across all columns
2. Ranked all features by mean absolute importance score
3. Plotted the **Elbow Curve** to identify the natural cut-off point
4. Selected the **top 21 features** for the optimized SVM model:

`MonthlyIncome` · `Age` · `TotalWorkingYears` · `DailyRate` · `YearsAtCompany` · `DistanceFromHome` · `EmployeeNumber` · `HourlyRate` · `MonthlyRate` · `YearsWithCurrManager` · `NumCompaniesWorked` · `YearsInCurrentRole` · `OverTime` · `PercentSalaryHike` · `StockOptionLevel` · `EnvironmentSatisfaction` · `JobLevel` · `JobSatisfaction` · `RelationshipSatisfaction` · `YearsSinceLastPromotion` · `WorkLifeBalance`

---

## 🏆 Final Model — SVM (RBF Kernel)

- SVM with RBF kernel achieved the best balance of **precision and recall** across all splits
- Trained on the **reduced 21-feature set** identified by the elbow method
- Evaluated at 20%, 30%, and 40% test splits for robustness
- Full metrics and confusion matrix available in `HR_attrition_report.pdf`

---

## 🔬 SHAP Explainability Analysis

SHAP (SHapley Additive exPlanations) was applied using `shap.TreeExplainer` on the XGBoost model to explain predictions at both global and individual employee levels.

**Three SHAP plot types generated:**

| Plot | Purpose |
|---|---|
| Bar summary plot | Overall feature importance ranking by mean absolute SHAP value |
| Beeswarm plot | Direction and magnitude of each feature's impact per employee |
| Dependence plot | Interaction between OverTime and Age on attrition risk |

**Top attrition drivers from SHAP:**

| Rank | Feature | Insight |
|---|---|---|
| 1 | OverTime_Yes | Biggest predictor — working overtime sharply increases attrition risk |
| 2 | StockOptionLevel | Low stock options push employees toward leaving |
| 3 | MonthlyIncome | Lower income increases resignation probability |
| 4 | Age | Younger employees leave more frequently |
| 5 | YearsWithCurrManager | Less time with current manager = higher risk |
| 6 | EnvironmentSatisfaction | Low satisfaction strongly increases attrition |
| 7 | WorkLifeBalance | Poor balance correlates with resignation |

> Full SHAP plots available in `shap_analysis.pdf`

---

## 📊 Power BI Dashboard

An interactive dashboard built to support business-level HR decision-making, covering:

- Department-wise attrition breakdown
- Demographic analysis — Age, Gender, Marital Status
- Compensation patterns vs attrition rates
- Career progression and promotion trends
- Satisfaction score distributions across departments

📁 Files: `HR_dashboard_1.pbix` · `PowerBI_Dashboard_Hr_attrition_proj....png`

---

## 💡 Business Recommendations

Based on model findings and SHAP analysis:

1. **Eliminate excessive overtime** — the single strongest attrition predictor; redistribute workloads and enforce overtime policies
2. **Revise compensation for lower income bands** — especially in Sales where attrition is highest
3. **Expand stock option programs** — employees with stock options show significantly higher retention
4. **Accelerate promotion timelines** — stagnation in role is a measurable attrition driver
5. **Introduce flexible/hybrid work options** — directly addresses the distance-from-home impact
6. **Invest in manager relationship programs** — short tenure under the same manager correlates with higher risk
7. **Run targeted engagement programs** for departments with low environment satisfaction scores

> Even a **1% reduction in attrition** across 1,470 employees translates to significant savings in recruitment, onboarding, and productivity loss costs.

---

## 🚀 Future Scope

- [ ] Deploy final SVM model as a **Streamlit web app** for live HR risk scoring
- [ ] Connect model to **real-time HR data pipelines**
- [ ] Explore **GridSearchCV hyperparameter tuning** for further optimization
- [ ] Add an **employee-level risk score API** for HR systems integration

---

## 🛠️ Tools & Technologies

- **Python** — Pandas, NumPy, Seaborn, Matplotlib
- **Machine Learning** — Scikit-Learn, XGBoost, CatBoost, SVM
- **Feature Selection** — Random Forest Importance, Elbow Method
- **Explainability** — SHAP (TreeExplainer)
- **Visualization** — Power BI
- **Environment** — Google Colab, Jupyter Notebook

---

## 👩‍💻 Author

**Peddi Praharshita**
