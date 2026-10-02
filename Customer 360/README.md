# Customer 360 — Machine Learning Project

## Project Overview

Customer 360 is a machine learning project that analyzes telecom customer data to build a complete view of customer behavior and value.

The project combines **exploratory data analysis, churn prediction, revenue prediction, customer segmentation, PCA, anomaly detection, and customer-level business insights** into one integrated Customer 360 solution.

The goal is to use historical customer information to identify churn risk, estimate future customer revenue, understand different customer segments, detect unusual customer profiles, and prioritize customers for potential retention actions.

---

## Dataset

The project uses the following dataset:

`customer_360_ml_workshop.csv`

The dataset contains **3,000 customers and 16 variables**, including demographic, usage, billing, service, satisfaction, revenue, and churn information.

Important fields include:

* `CustomerID`
* `Age`
* `Region`
* `TenureMonths`
* `ContractType`
* `InternetType`
* `MonthlyUsageGB`
* `MonthlyChargeEGP`
* `NumServices`
* `SupportCalls6M`
* `LatePayments12M`
* `PaperlessBilling`
* `AutoPay`
* `SatisfactionScore`
* `Future12MRevenueEGP`
* `Churn`

### Important Modeling Decisions

* `CustomerID` is treated as an identifier and is excluded from machine learning features.
* `Future12MRevenueEGP` is excluded from current churn prediction because it represents a future outcome and could cause data leakage.
* Missing values are handled through preprocessing pipelines.
* Categorical variables are encoded using one-hot encoding.
* Numerical variables are standardized when required by scale-sensitive algorithms.
* `random_state=42` is used where applicable for reproducibility.

---

## Project Structure

```text
Customer-360/
│
├── README.md
│
├── data/
│   └── customer_360_ml_workshop.csv
│
├── notebooks/
│   ├── 01_eda.ipynb
│   ├── 02_churn_modeling.ipynb
│   ├── 03_revenue_modeling.ipynb
│   ├── 04_customer_segmentation.ipynb
│   └── 05_customer_360.ipynb
│
├── models/
│   ├── churn_model.pkl
│   ├── revenue_model.pkl
│   └── segmentation_model.pkl
│
└── outputs/
    └── customer_360_predictions.csv
```

---

## Project Notebooks

### 1. Exploratory Data Analysis — `01_eda.ipynb`

This notebook explores the dataset structure, data quality, missing values, customer characteristics, churn distribution, numerical variables, and relationships between customer attributes and churn.

The EDA findings are used to guide the preprocessing and modeling stages.

### 2. Churn Prediction — `02_churn_modeling.ipynb`

This notebook develops machine learning classification models to predict whether a customer is likely to churn.

The models include:

* Logistic Regression
* K-Nearest Neighbors
* Decision Tree
* Random Forest
* Support Vector Machine
* Naive Bayes
* Gradient Boosting

Models are evaluated using:

* Accuracy
* Precision
* Recall
* F1-score
* ROC-AUC

The Random Forest model is further tuned using GridSearchCV.

### 3. Revenue Prediction — `03_revenue_modeling.ipynb`

This notebook predicts customers' future 12-month revenue using regression techniques.

The models include:

* Linear Regression
* Ridge Regression
* Lasso Regression
* KNN Regressor
* Decision Tree Regressor
* Random Forest Regressor
* Gradient Boosting Regressor

Models are evaluated using:

* MAE
* RMSE
* R²

### 4. Customer Segmentation — `04_customer_segmentation.ipynb`

This notebook identifies groups of customers with similar behavioral and service characteristics.

The segmentation analysis uses:

* K-Means
* Agglomerative Clustering
* DBSCAN

The notebook evaluates different clustering configurations using measures such as inertia and silhouette score.

PCA is also used to visualize customer groups, while Isolation Forest is used to identify unusual customer profiles.

### 5. Customer 360 — `05_customer_360.ipynb`

This notebook integrates the outputs from the previous analyses into a single customer-level view.

The final Customer 360 table contains:

* Customer ID
* Churn probability
* Predicted 12-month revenue
* Customer segment
* Anomaly flag
* Retention-priority flag

The final results are exported to:

`outputs/customer_360_predictions.csv`

---

## Customer 360 Integration

The final Customer 360 solution combines four perspectives:

**Churn Risk + Customer Value + Customer Segment + Anomaly Status**

This allows customers to be analyzed not only by their probability of churn, but also by their predicted future value and behavioral characteristics.

The retention-priority rule combines churn risk with customer value so that customers with higher churn probability and relatively high predicted revenue can be identified for further retention consideration.

This rule is intended as an analytical prioritization mechanism rather than an automatic decision.

---

## Machine Learning Workflow

The overall workflow is:

```text
Raw Customer Data
        ↓
Exploratory Data Analysis
        ↓
Data Preprocessing
        ↓
Churn Prediction ──────────┐
                            │
Revenue Prediction ────────┤
                            ├──→ Customer 360
Customer Segmentation ─────┤
                            │
PCA & Anomaly Detection ───┘
        ↓
Business Insights
```

---

## Expected Outputs

The project produces:

* EDA visualizations and findings
* Classification model comparison
* Churn confusion matrix and ROC curve
* Tuned Random Forest model
* Important churn predictors
* Regression model comparison
* Actual vs. predicted revenue visualization
* Customer cluster analysis and profiles
* PCA visualization
* Anomaly analysis
* Integrated Customer 360 dataset
* Retention-priority customer identification

---

## Key Business Applications

The analysis can support several business activities:

1. **Retention planning**
   Identify customers with higher predicted churn risk for proactive review.

2. **Customer value analysis**
   Combine churn risk with predicted future revenue to understand potential customer value.

3. **Customer segmentation**
   Develop different strategies for different behavioral customer groups.

4. **Unusual customer investigation**
   Review customers whose behavior differs substantially from typical customer profiles.

5. **Customer 360 decision support**
   Combine multiple machine learning outputs into one customer-level analytical view.

---

## How to Run the Project

1. Place the dataset inside the `data/` folder.
2. Open the notebooks in the `notebooks/` folder.
3. Run the notebooks in the following order:

```text
01_eda.ipynb
      ↓
02_churn_modeling.ipynb
      ↓
03_revenue_modeling.ipynb
      ↓
04_customer_segmentation.ipynb
      ↓
05_customer_360.ipynb
```

4. Ensure the required model files are created in the `models/` folder.
5. Run the final Customer 360 notebook.
6. Check the generated results in the `outputs/` folder.

---

## Reproducibility

The project uses a fixed random seed (`random_state=42`) where applicable.

The preprocessing steps are designed to prevent information leakage by fitting transformations on the training data before applying them to unseen data.

The test set should remain untouched during model selection and hyperparameter tuning.

---

## Final Deliverable

The main final output of the project is:

```text
outputs/customer_360_predictions.csv
```

This file provides an integrated customer-level view that combines predictive modeling, segmentation, and anomaly detection results.

---

## Conclusion

The Customer 360 project demonstrates how supervised and unsupervised machine learning techniques can be combined to analyze customer behavior from multiple perspectives.

Rather than relying on a single model, the project integrates **churn risk, predicted revenue, customer segmentation, and anomaly detection** to create a more complete analytical view of the customer base.