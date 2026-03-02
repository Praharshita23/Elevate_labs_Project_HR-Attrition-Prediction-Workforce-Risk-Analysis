**HR Attrition Prediction & Workforce Risk Analysis**

This project analyzes employee data to understand the main causes of attrition and builds predictive machine learning models to identify employees at risk of leaving.

The objective is to help HR teams make proactive, data-driven retention decisions.

**Problem Statement
**
Employee attrition reduces productivity and increases recruitment costs.

Organizations often react after employees resign.

This project aims to:

Identify key drivers of attrition

Build classification models to predict resignation probability

Provide actionable HR recommendations

Support strategic workforce planning

**Dataset Overview
**
Dataset: IBM HR Employee Attrition Dataset

1470 employee records

35 HR-related features

Attrition rate: 16.12%

Data Includes:

Demographics (Age, Gender, Marital Status)

Job Role & Department

Compensation (Monthly Income, Salary Hike, Stock Options)

**Data Preprocessing
**
Removed irrelevant columns

Checked missing values

Encoded categorical variables

Scaled numerical features

Applied stratified train-test splitting

**Exploratory Data Analysis
**
Key insights from EDA:

Sales roles show higher attrition

Employees with less than 5 years tenure are more likely to leave

Overtime increases resignation probability

Long commute distance impacts retention

Low job satisfaction strongly correlates with attrition

Correlation heatmaps and distribution plots were used to analyze feature relationships.

**Machine Learning Models Implemented
**
The following models were trained and evaluated:

Logistic Regression

Random Forest

XGBoost

CatBoost

Support Vector Machine (SVM)

Evaluation Metrics:

Accuracy

Precision

Recall

F1-Score

ROC-AUC

**Final Model
**
SVM achieved the best balance between precision and recall.

Feature selection was performed using Random Forest importance and the elbow method.

The optimized SVM model achieved strong predictive performance with reduced feature complexity.

**Key Drivers of Attrition
**
Top influencing features:

Monthly Income

Years at Company

Age & Total Working Years

Overtime

Job Satisfaction

These indicate that compensation, career growth, and work-life balance strongly affect retention.

**Power BI Dashboard
**
An interactive Power BI dashboard was developed to visualize:

Department-wise attrition

Demographic analysis

Compensation analysis

Career progression patterns

Satisfaction trends

This supports business-level decision-making.

**Business Recommendations
**
Based on analysis:

Strengthen promotion pathways

Reduce excessive overtime

Introduce flexible work options

Implement performance-based salary increments

Even a small reduction in attrition can significantly reduce hiring and training costs.

**Future Scope
**
Deploy model using Streamlit

Integrate SHAP for explainability

Connect model with real-time HR dashboards

Explore advanced ensemble optimization

**Author**

Peddi Praharshita

Work Conditions (Overtime, Distance from Home)

Satisfaction Scores (Job, Environment, Relationship)
