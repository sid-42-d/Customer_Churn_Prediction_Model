# Telco Customer Churn Analysis & Prediction

## 📌 Executive Summary
This project analyzes customer attrition for a telecommunications provider using a dataset of **7,032 customer records** across **20 feature attributes** (after cleaning). By combining Exploratory Data Analysis (EDA) and Machine Learning techniques, this model identifies key drivers of churn and provides predictive insights to optimize customer retention strategies.

---

## 🛠️ Tech Stack & Dependencies

* **Language:** Python 3.x
* **Environment:** Google Colab / Jupyter Notebook
* **Data Processing & Manipulation:** `pandas`, `numpy`
* **Data Visualization:** `matplotlib`, `seaborn`, `plotly`, `missingno`
* **Machine Learning & Preprocessing:** `scikit-learn` (`LabelEncoder`, `StandardScaler`, `train_test_split`, classification models & metrics)

---

## 🧹 Data Cleaning & Preprocessing

* **Zero-Tenure & Missing Data Removal:** Identified 11 rows where `tenure == 0`, `Churn` was `"No"`, and `TotalCharges` contained missing/empty string values (`""`). These represent new accounts with no prior billing cycle or revenue history. All 11 rows were dropped to prevent the model from learning inaccurate patterns.
* **Feature Selection:** Removed non-informative identifier columns (`customerID`).
* **Feature Encoding Strategy:**
  * **Categorical & Binary Features:** Converted categorical attributes to numeric values using `sklearn.preprocessing.LabelEncoder`.
  * *Rationale:* While Label Encoding can introduce unintended ordinality, tree-based models (e.g., Random Forest, Gradient Boosting) are invariant to monotonic transformations. Label Encoding was selected over One-Hot Encoding to avoid introducing high dimensionality into the dataset.
* **Feature Scaling:** Continuous numerical variables (`tenure`, `MonthlyCharges`, `TotalCharges`) spanned wide value ranges and were standardized using Z-score normalization (`StandardScaler`) on a 70:30 Train/Test split.

---

## 📊 Dataset & Features
The dataset evaluates customer demographics, subscribed services, account parameters, and total spending:
* **Demographics:** Gender, Senior Citizen status, Partner status, Dependents.
* **Services:** Phone Service, Multiple Lines, Internet Service (DSL / Fiber Optic), Online Security, Online Backup, Device Protection, Tech Support, Streaming TV, Streaming Movies.
* **Account Info:** Tenure (months), Contract type (Month-to-month, One year, Two year), Paperless Billing, Payment Method, Monthly Charges, Total Charges.
* **Target Variable:** `Churn` (Yes = 1 / No = 0).

---

## 🔍 Key Findings & Exploratory Insights

### 1. Overall Retention & Demographics
* **Baseline Churn:** The company successfully retains **73.4%** of its customer base, while overall churn stands at **26.6%**.
* **Senior Citizens:** A significantly larger proportion of churned customers are senior citizens compared to those who remain.
* **Partners & Dependents:** Customers with partners or dependents show markedly higher retention. Reducing entry barriers for partner or family add-on packages presents a key opportunity to reduce churn.

### 2. Contract Types & Payment Channels
* **Contract Length:** 
  * **~70%** of customers on **Month-to-Month** contracts leave the company.
  * **<15%** of customers on **One-Year** contracts churn.
  * **<4%** of customers on **Two-Year** contracts churn.
* **Payment Methods:**
  * **~82%** of customers paying via **Electronic Check** churned.
  * **<17%** of customers using automatic **Credit Card** payments churned.
  * **<18%** of customers using automatic **Bank Transfer** churned.
  * **23%** of customers paying via **Mailed Check** churned.

### 3. Add-on & Technical Support Services
* **Online Security:** **~72%** of internet subscribers without Online Security churned, compared to only **17%** of those who opted in.
* **Online Backup:** **~64%** of customers without Online Backup churned, compared to **~26%** of those who opted in.
* **Tech Support:** **~70%** of customers without Technical Support churned, compared to **17%** of those with Tech Support.
* **No Internet Service:** Across all value-added service categories, only **~7%** of customers without internet service churned.

---

## 📐 Evaluation Metrics & Business Strategy

The dataset uses a **70:30 Train/Test Split**. Models are evaluated across multiple metrics to balance customer acquisition costs against targeted retention spending:

| Metric | Business Definition & Purpose | Strategic Value |
| :--- | :--- | :--- |
| **ROC-AUC** | Area Under Receiver Operating Characteristic Curve | Primary metric measuring overall class separability across all threshold levels. |
| **Recall (Sensitivity)** | $\frac{\text{True Positives}}{\text{True Positives} + \text{False Negatives}}$ | High priority to minimize missed high-risk churners (false negatives). |
| **Precision** | $\frac{\text{True Positives}}{\text{True Positives} + \text{False Positives}}$ | Controls unnecessary retention spend on safe customers incorrectly flagged as high-risk. |
| **F1-Score** | Harmonic mean of Precision and Recall | Measures overall performance balance given the dataset's class imbalance (~26.6% churn rate). |
| **Accuracy** | Baseline ratio of total correct predictions | Provides standard overall predictive accuracy. |

---

## 💡 Strategic Recommendations
1. **Incentivize Long-Term Contracts:** Offer targeted discounts or loyalty perks to convert high-risk Month-to-Month subscribers into 1-year or 2-year plans.
2. **Promote Automatic Payments:** Actively encourage customers using Electronic Checks to transition to automatic Bank Transfers or Credit Card payments.
3. **Bundle Value-Added Services:** Package **Online Security**, **Online Backup**, and **Tech Support** into baseline internet tiers to significantly boost customer retention.
4. **Partner & Family Plans:** Lower the cost of adding partners or dependents to accounts to leverage strong demographic retention patterns.
