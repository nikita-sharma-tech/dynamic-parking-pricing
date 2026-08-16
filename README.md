# Dynamic Pricing for Urban Parking Lots

An end-to-end **Data Science and Machine Learning project** that forecasts parking occupancy and uses predicted demand to develop a dynamic pricing strategy for urban parking facilities.

The project covers **data cleaning, EDA, feature engineering, demand forecasting, XGBoost regression, dynamic pricing, revenue simulation, sensitivity analysis, and SHAP explainability**.

---

##  Problem Statement

Parking demand changes significantly throughout the day and across different parking facilities.

The objective of this project is to:

- Predict future parking occupancy
- Identify parking demand levels
- Dynamically adjust parking prices based on predicted demand
- Compare static and dynamic pricing strategies
- Analyze the potential business impact of dynamic pricing
- Explain the ML model using SHAP

---

##  Project Workflow

```text
Raw Parking Data
       ↓
Data Cleaning
       ↓
Exploratory Data Analysis
       ↓
Feature Engineering
       ↓
Demand Forecasting
       ↓
XGBoost Regression
       ↓
Predicted Occupancy
       ↓
Demand Score
       ↓
Dynamic Pricing
       ↓
Revenue Simulation
       ↓
Sensitivity Analysis
       ↓
SHAP Explainability

```

##  Project Structure

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

```

##  Dataset

The project uses the **Birmingham Parking Dataset**, containing historical parking occupancy information from multiple parking facilities.

The main variables include:

- Parking facility
- Timestamp
- Parking capacity
- Parking occupancy

The raw dataset is not included in the GitHub repository.

---

##  Data Cleaning

The data preprocessing pipeline includes:

- Handling missing values
- Removing duplicate records
- Converting timestamps to datetime
- Detecting invalid occupancy values
- Handling occupancy values below zero
- Handling occupancy values greater than parking capacity
- Sorting records chronologically

---

##  Exploratory Data Analysis

EDA was performed to understand parking demand patterns, including:

- Occupancy distribution
- Parking utilization
- Peak occupancy periods
- Hourly demand patterns
- Daily demand patterns
- Parking-lot-level demand
- Available parking spaces
- Time-based demand trends

---

##  Feature Engineering

Several features were created to capture temporal and demand-related patterns.

### Time Features

- Hour
- Minute
- Day of Week
- Weekend Indicator

### Cyclical Features

- Hour Sine
- Hour Cosine
- Day Sine
- Day Cosine

### Lag Features

- Occupancy Lag 1
- Occupancy Lag 2
- Occupancy Lag 3
- Occupancy Rate Lag 1
- Occupancy Rate Lag 2

### Rolling Features

- Rolling Mean
- Rolling Standard Deviation

### Additional Features

- Occupancy Rate
- Available Spaces
- Occupancy Change
- Demand Momentum

---

##  Machine Learning

Multiple regression models were evaluated for parking occupancy forecasting.

### Final Model

**XGBoost Regressor**

XGBoost was selected because it can capture nonlinear relationships between historical occupancy, temporal patterns, parking capacity, and recent demand behavior.

The trained model is saved at:

```text
models/demand_model.pkl

```

##  Dynamic Pricing

The predicted parking occupancy is converted into a demand score, which is then used to determine the appropriate parking price.

### Pricing Range

| Parameter | Value |
|---|---:|
| Minimum Price | ₹8 |
| Base Price | ₹10 |
| Maximum Price | ₹16 |

The pricing strategy follows:

```text
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

```

##  Demand Classification

The predicted parking occupancy is classified into four demand levels:

| Demand Level | Predicted Occupancy |
|---|---:|
| Low | < 30% |
| Moderate | 30% – 60% |
| High | 60% – 80% |
| Critical | ≥ 80% |

This classification helps translate ML predictions into an understandable business decision.



##  Business Simulation

The project compares two pricing strategies:

### Static Pricing

A fixed parking price of ₹10 is used as the baseline.

### Dynamic Pricing

The parking price changes according to predicted parking demand.

```text
Predicted Occupancy
        ↓
Demand Score
        ↓
Dynamic Price
        ↓
Simulated Demand Response
        ↓
Revenue
```

##  Sensitivity Analysis

The dataset does not contain historical parking prices or customer-level price-response information.

Therefore, actual price elasticity cannot be directly estimated from the available data.

Instead, multiple assumed price-elasticity values are tested to evaluate the robustness of the dynamic pricing strategy.

Example elasticity scenarios:

```text
0.05
0.10
0.15
0.20
0.25
0.30

```

##  Model Explainability

SHAP (SHapley Additive exPlanations) is used to interpret the final XGBoost demand forecasting model.

The explainability analysis helps identify which features have the greatest influence on parking occupancy predictions.

The analysis includes:

- Global feature importance
- SHAP summary plot
- Feature contribution analysis
- Individual prediction explanations
- SHAP feature importance

Generated outputs are stored in:

```text
output/
├── shap_feature_importance.csv
├── shap_feature_importance.png
└── shap_summary_plot.png

```
##  How to Run

### 1. Clone the Repository

```bash
git clone https://github.com/nikita-sharma-tech/dynamic-parking-pricing.git
```

### 2. Navigate to the Project Directory

```bash
cd dynamic-parking-pricing
```

### 3. Create a Virtual Environment

```bash
python -m venv venv
```

### 4. Activate the Virtual Environment

#### Windows

```bash
venv\Scripts\activate
```

#### macOS / Linux

```bash
source venv/bin/activate
```

### 5. Install Dependencies

```bash
pip install -r requirements.txt
```

### 6. Start Jupyter Notebook

```bash
jupyter notebook
```

Run the notebooks in the following order:

1. `01_data_cleaning_ipynb.ipynb`
2. `02_eda.ipynb`
3. `03_feature_engineering.ipynb`
4. `04_demand_forecasting.ipynb`
5. `05_dynamic_pricing.ipynb`
6. `06_model_interpretation.ipynb`

---

##  Key Outputs

The project generates:

- Cleaned parking dataset
- Engineered feature dataset
- Parking occupancy predictions
- Demand scores
- Demand classifications
- Dynamic parking prices
- Static pricing results
- Dynamic pricing results
- Revenue simulation
- Sensitivity analysis
- XGBoost model
- SHAP feature importance
- SHAP visualizations

Important generated files:

- `models/demand_model.pkl`
- `data/processed/dynamic_pricing_results.csv`
- `output/shap_feature_importance.csv`
- `output/shap_feature_importance.png`
- `output/shap_summary_plot.png`

---

##  Limitations

This project is a Machine Learning and business simulation framework rather than a production pricing system.

The dataset does not contain:

- Historical parking prices
- Customer transaction data
- Customer willingness-to-pay
- Observed price elasticity
- Actual parking revenue

Therefore, revenue and demand-response results are simulation-based and depend on assumed price-elasticity values.

A production system would require real pricing and transaction data to estimate customer price sensitivity empirically.

---

##  Future Improvements

- Learn price elasticity from real transaction data
- Incorporate weather information
- Incorporate holidays and special events
- Add real-time occupancy forecasting
- Build a real-time dynamic pricing API
- Add model monitoring
- Explore reinforcement-learning-based pricing
- Deploy the system to the cloud
- Perform real-world A/B testing
- Build an interactive dashboard for parking operators

---

##  Author

**Nikita Sharma**

B.Tech Computer Science Engineering  
Specialization: Data Science & Artificial Intelligence

---


