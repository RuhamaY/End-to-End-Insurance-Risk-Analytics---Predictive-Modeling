## 📄 `README.md`

```markdown
# 🚗 ACIS Car Insurance Analytics Challenge

This repository contains my full submission for the **AlphaCare Insurance Solutions (ACIS)** Insurance Analytics Challenge (June 2025), focused on car insurance planning and marketing in South Africa. 

The project includes:
- Exploratory Data Analysis (EDA)
- Data Version Control (DVC)
- A/B hypothesis testing
- Predictive modeling for claim severity and premium optimization

---

## 📊 Project Objectives

AlphaCare seeks to improve its marketing and pricing strategy by:
- Discovering low-risk policyholders who can be offered lower premiums
- Understanding geographic, demographic, and vehicle-related claim patterns
- Developing risk-based pricing through machine learning

---

## 🧱 Project Structure


acis-insurance-eda/
├── data/                         # Raw or processed datasets (tracked by DVC)
│   └── insurance.csv
├── notebooks/                    # Analysis notebooks per task
│   ├── task1\_eda\_analysis.ipynb
│   ├── task3\_hypothesis\_tests.ipynb
│   └── task4\_modeling.ipynb
├── plots/                        # Visualizations used in reporting
│   ├── loss\_ratio\_by\_province.png
│   └── ...
├── reports/                      # Summaries or markdowns
│   ├── task1\_summary.md
│   ├── task3\_findings.md
│   └── final\_blog\_post.md
├── .dvc/                         # DVC tracking files
├── .gitignore
├── README.md
├── requirements.txt


---

## 🧠 Tasks & Deliverables

### ✅ Task 1: Exploratory Data Analysis (EDA)

- Data structure review, null value check
- Descriptive statistics for TotalPremium, TotalClaims, CustomValueEstimate
- Distribution analysis (histograms, boxplots)
- Bivariate relationships (Loss Ratio by Province, Gender, etc.)
- Trend analysis over 18 months
- Outlier detection
- 3 key visualizations saved in `plots/`

📍**Key Insight**: Gauteng shows significantly higher loss ratios than other provinces, especially among high-end vehicle types.

---

### ✅ Task 2: Data Version Control (DVC)

- Initialized DVC
- Created local remote storage and added dataset using:
  ```bash
  dvc init
  dvc remote add -d localstorage /path/to/storage
  dvc add data/insurance.csv
  dvc push
````

* Dataset is fully versioned and reproducible.

📍**Benefit**: Enables complete auditability of results and consistent experimentation.

---

### ✅ Task 3: A/B Hypothesis Testing

**Hypotheses tested**:

* H₀: No risk differences across provinces ✅ *rejected*
* H₀: No risk differences between zip codes ✅ *rejected*
* H₀: No margin difference between zip codes ❌ *not rejected*
* H₀: No risk difference between women and men ❌ *not rejected*

**Tests Used**:

* ANOVA
* T-tests / Welch’s test
* Chi-squared test
* Effect size measures (Cohen’s d)

📍**Business Implication**: Risk-based segmentation is valid by **region**, but not strongly justified by gender. Zipcode-level risk segmentation needs further refinement.

---

### ✅ Task 4: Predictive Modeling

#### 1. Risk (Claim Severity) Model

* Target: `TotalClaims` where claims > 0
* Models used:

  * Linear Regression
  * Random Forest Regressor
  * XGBoost Regressor
* Metrics:

  * RMSE, R²
* Interpretation: SHAP used to analyze top features

#### 2. Premium Prediction Model

* Target: `CalculatedPremiumPerTerm`
* Combined risk score using:

  ```
  Premium = P(Claim) * Expected Claim + Expense + Margin
  ```

#### 3. Binary Classifier for Claim Probability

* Target: Binary `claim_occurred` (TotalClaims > 0)
* Models:

  * Logistic Regression
  * Random Forest Classifier
  * XGBoost Classifier
* Metrics:

  * Accuracy, AUC, Precision, Recall, F1

📍**Insight**:

* Key risk factors include:

  * `Province`, `VehicleType`, `Make`, `CustomValueEstimate`, and `NumberOfVehiclesInFleet`
* Older vehicles and high-value makes (BMW, Audi) predict higher claims.

---

## 📦 How to Run

### 1. Clone the Repository

```bash
git clone https://github.com/<your-username>/acis-insurance-eda.git
cd acis-insurance-eda
```

### 2. Install Requirements

```bash
python -m venv venv
source venv/bin/activate     # or venv\Scripts\activate on Windows
pip install -r requirements.txt
```

### 3. Setup DVC (if needed)

```bash
dvc pull       # fetch data from local or remote storage
```

### 4. Launch Notebooks

```bash
jupyter notebook
```

---

## 📌 Results Summary

| Task               | Key Insight                                                    |
| ------------------ | -------------------------------------------------------------- |
| EDA                | High risk in Gauteng, skewed claim amounts                     |
| DVC                | Enables full versioning and reproducibility                    |
| Hypothesis Testing | Risk varies by region, not gender                              |
| Modeling           | Premiums should reflect vehicle type, region, and risk history |

---

## 💡 Suggestions for ACIS

1. Use **region-based pricing** adjustments, especially in high-claim provinces.
2. Avoid gender-based pricing — statistically insignificant.
3. Target **low-value, low-fleet vehicles** in safer provinces for discounted premiums.
4. Invest in real-time vehicle risk scoring using enriched features like telematics.

---

## 📅 Timeline

* 🗓️ Challenge Start: June 11, 2025
* 📥 Interim Submission: June 16, 2025
* 📤 Final Submission: June 17, 2025

---

