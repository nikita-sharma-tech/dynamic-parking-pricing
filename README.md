# Dynamic Pricing for Urban Parking Lots

An end-to-end Data Science project that uses Machine Learning to forecast parking occupancy and develop a demand-driven dynamic pricing strategy for urban parking facilities.

The project combines data cleaning, exploratory data analysis, time-based feature engineering, occupancy forecasting, XGBoost regression, dynamic pricing, business simulation, sensitivity analysis, and SHAP-based model explainability.

---

## Project Overview

Urban parking demand changes throughout the day depending on time, historical occupancy, parking capacity, and recent demand patterns.

A fixed parking price does not adapt to these fluctuations.

This project develops an ML-driven framework that forecasts near-term parking occupancy and converts predicted demand into a dynamic parking price.

### Main Pipeline

Historical Parking Data
        ↓
Data Cleaning
        ↓
Exploratory Data Analysis
        ↓
Feature Engineering
        ↓
Occupancy Forecasting
        ↓
XGBoost Regression
        ↓
Predicted Occupancy
        ↓
Demand Score
        ↓
Dynamic Pricing
        ↓
Revenue & Utilization Simulation
        ↓
Sensitivity Analysis
        ↓
SHAP Explainability

---

## Problem Statement

The objective is to build a Machine Learning system capable of predicting parking occupancy and using the predicted demand to support dynamic pricing decisions.

### Business Question

> Can Machine Learning-based demand forecasting be used to design a dynamic parking pricing strategy that responds to changing parking demand?

---

## Dataset

The project uses the Birmingham parking dataset containing historical parking occupancy information from multiple parking facilities.

The dataset contains information related to:

- Parking facility
- Timestamp
- Parking capacity
- Parking occupancy

The raw dataset is not included in the GitHub repository.

---

# Project Structure

```text
dynamic-parking-pricing/
│
├── data/
│   ├── processed/
│   │   ├── dynamic_pricing_results.csv
│   │   ├── parking_cleaned.csv
│   │   └── parking_features.csv
│   │
│   └── raw/
│       └── parking.csv
│
├── models/
│   └── demand_model.pkl
│
├── notebooks/
│   ├── 01_data_cleaning_ipynb.ipynb
│   ├── 02_eda.ipynb
│   ├── 03_feature_engineering.ipynb
│   ├── 04_demand_forecasting.ipynb
│   ├── 05_dynamic_pricing.ipynb
│   └── 06_model_interpretation.ipynb
│
├── output/
│   ├── shap_feature_importance.csv
│   ├── shap_feature_importance.png
│   └── shap_summary_plot.png
│
├── README.md
├── requirements.txt
└── .gitignore

# Methodology

## 1. Data Cleaning

The raw parking data was cleaned and prepared for analysis by:

- Handling missing values
- Removing duplicate records
- Converting timestamp columns to datetime format
- Checking invalid occupancy values
- Handling occupancy values below zero
- Handling occupancy values greater than parking capacity
- Sorting records chronologically
- Creating a cleaned dataset for further analysis

---

## 2. Exploratory Data Analysis

Exploratory Data Analysis (EDA) was performed to understand parking demand patterns.

The analysis included:

- Occupancy distribution
- Parking utilization
- Hourly occupancy patterns
- Daily occupancy patterns
- Parking-lot-level demand
- Peak occupancy periods
- Available parking spaces
- Time-based demand trends

---

## 3. Feature Engineering

Several features were created to help the Machine Learning model capture temporal and demand-related patterns.

### Time-Based Features

- Hour
- Minute
- Day of Week
- Weekend Indicator

### Cyclical Features

- Hour Sine
- Hour Cosine
- Day Sine
- Day Cosine

Cyclical encoding helps the model understand that time is periodic. For example, 23:00 and 00:00 are close in time even though their numerical values are far apart.

### Lag Features

Historical occupancy information was captured using lag features such as:

- Occupancy Lag 1
- Occupancy Lag 2
- Occupancy Lag 3
- Occupancy Rate Lag 1
- Occupancy Rate Lag 2

### Rolling Features

Recent occupancy trends were captured using:

- Rolling Mean
- Rolling Standard Deviation

### Additional Features

- Occupancy Rate
- Available Spaces
- Occupancy Change
- Demand Momentum

---

# Machine Learning

## 4. Demand Forecasting

The objective of the forecasting stage is to predict future parking occupancy using historical parking information and engineered features.

The project evaluates multiple regression models before selecting the final model.

### Final Model

**XGBoost Regressor**

XGBoost was selected because it can capture nonlinear relationships between:

- Historical occupancy
- Parking capacity
- Time-based patterns
- Recent demand trends
- Occupancy-related features

The trained model is saved as:

```text
models/demand_model.pkl

5. Model Evaluation

The forecasting models were evaluated using standard regression metrics:

MAE

Mean Absolute Error measures the average absolute difference between actual and predicted occupancy.

RMSE

Root Mean Squared Error gives greater importance to larger prediction errors.

R² Score

R² measures how much of the variation in the target variable is explained by the model.

The complete model comparison and evaluation can be found in:

notebooks/04_demand_forecasting.ipynb
Dynamic Pricing
6. Demand Score

The predicted occupancy is converted into a normalized demand score.

The demand score combines predicted occupancy information with recent demand behavior.

The resulting score ranges from:

0 → Low Demand
1 → Very High Demand

This score is then used as an input to the dynamic pricing strategy.

7. Dynamic Pricing Strategy

The project uses demand intensity to dynamically adjust the parking price.

The simulated pricing range is:

Pricing Parameter	Value
Minimum Price	₹8
Base Price	₹10
Maximum Price	₹16

The basic pricing relationship is:

Low Demand
    ↓
Lower Price


Moderate Demand
    ↓
Near Base Price


High Demand
    ↓
Higher Price


Critical Demand
    ↓
Maximum Price

This allows parking prices to respond to changing demand conditions.

8. Demand Classification

Predicted parking demand is classified into four levels:

Demand Level	Predicted Occupancy
Low	< 30%
Moderate	30% – 60%
High	60% – 80%
Critical	≥ 80%

The classification helps translate the ML predictions into an interpretable operational decision.

Business Simulation
9. Static vs Dynamic Pricing

The project compares two pricing strategies.

Static Pricing

A fixed parking price of ₹10 is used as the baseline.

Fixed Price
    ↓
Parking Demand
    ↓
Revenue
Dynamic Pricing

The dynamic strategy adjusts the price according to predicted demand.

Predicted Occupancy
        ↓
Demand Score
        ↓
Dynamic Price
        ↓
Simulated Demand Response
        ↓
Revenue
10. Revenue Simulation

The original dataset does not contain historical parking prices or customer-level price-response information.

Therefore, actual price elasticity cannot be directly learned from the available data.

Instead, the project simulates demand response using assumed price-elasticity values.

The simulation evaluates:

Revenue
Parking utilization
Occupancy levels
Critical demand periods
Static vs dynamic pricing performance

The generated pricing results are stored in:

data/processed/dynamic_pricing_results.csv
11. Sensitivity Analysis

Sensitivity analysis is performed to evaluate the robustness of the dynamic pricing strategy under different price-elasticity assumptions.

Multiple elasticity values are tested, including:

0.05
0.10
0.15
0.20
0.25
0.30

This helps determine whether the pricing strategy remains effective when customer price sensitivity changes.

Model Explainability
12. SHAP Explainability

SHAP (SHapley Additive exPlanations) is used to interpret the XGBoost model.

The analysis helps answer:

Which features are driving the model's parking occupancy predictions?

The project includes:

Global feature importance
SHAP summary plot
SHAP feature importance
Feature contribution analysis
Individual prediction interpretation
SHAP dependence analysis
13. SHAP Feature Importance

The SHAP feature importance results are stored in:

output/shap_feature_importance.csv

Visualizations are available in:

output/shap_feature_importance.png
output/shap_summary_plot.png

The complete explainability workflow is available in:

notebooks/06_model_interpretation.ipynb
Key Results

The project produces the following outputs:

Predicted parking occupancy
Predicted occupancy rate
Demand score
Demand category
Dynamic parking price
Static pricing results
Dynamic pricing results
Revenue simulation
Parking utilization analysis
Sensitivity analysis
XGBoost feature importance
SHAP feature importance
SHAP visualizations
Technologies Used
Programming Language
Python
Data Processing
Pandas
NumPy
Data Visualization
Matplotlib
Seaborn
Machine Learning
Scikit-learn
XGBoost
Explainable AI
SHAP
Model Persistence
Joblib
Development Tools
Jupyter Notebook
Git
GitHub
How to Run the Project

# How to Run the Project

## 1. Clone the Repository

Clone this repository to your local machine:

```bash
git clone https://github.com/YOUR_USERNAME/dynamic-parking-pricing.git

## 2. Navigate to the Project Directory
cd dynamic-parking-pricing

## 3. Create a Virtual Environment

Create a Python virtual environment:
python -m venv venv

## 4. Install Required Dependencies

Install all required Python libraries using:

pip install -r requirements.txt

Author

Nikita Sharma

B.Tech Computer Science Engineering
Specialization: Data Science & Artificial Intelligence
