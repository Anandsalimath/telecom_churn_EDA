# Telco Customer Churn - Exploratory Data Analysis Project

## Project Overview

This project performs an in-depth exploratory data analysis (EDA) on the Telco Customer Churn dataset to understand the key factors that drive customer attrition. The analysis identifies actionable patterns and provides business recommendations to reduce churn rates.

## Dataset

**Source:** Telco Customer Churn CSV (`WA_Fn-UseC_-Telco-Customer-Churn.csv`)

**Size:** 7,043 customer records across 21 variables

**Target Variable:** `Churn` (Yes/No)

### Key Features:
- **Demographics:** gender, SeniorCitizen, Partner, Dependents
- **Account Information:** customerID, tenure (months with company)
- **Services:** PhoneService, MultipleLines, InternetService (DSL/Fiber optic/No), OnlineSecurity, OnlineBackup, DeviceProtection, TechSupport, StreamingTV, StreamingMovies
- **Billing:** Contract (Month-to-month/One year/Two year), PaperlessBilling, PaymentMethod, MonthlyCharges, TotalCharges


## Requirements

### Python Libraries:
```python
pandas==2.x
numpy==1.x
matplotlib==3.x
seaborn==0.12+
scipy==1.x
scikit-learn==1.x
```

### Installation:
```bash
pip install pandas numpy matplotlib seaborn scipy scikit-learn
```

Or install from requirements file:
```bash
pip install -r requirements.txt
```

## Analysis Workflow

### 1. Data Import and Initial Profiling
- Load dataset using pandas
- Inspect structure: shape, data types, basic statistics
- Create custom summary function (UDF) for comprehensive overview

### 2. Data Cleaning
- Handle missing `TotalCharges` values (11 records with blanks → dropped)
- Convert data types appropriately (categorical vs numeric)
- Check for duplicate customer IDs (none found)
- Implement IQR-based outlier detection function

### 3. Feature Engineering

**Advanced Python Techniques Demonstrated:**

- **Lambda Functions:**
  - `ChurnFlag`: Convert Churn (Yes/No) to binary (1/0)
  - `TenureGroup`: Categorize tenure into New/Recent/Established/Loyal

- **User-Defined Functions (UDF):**
  - `detailed_summary()`: Generate comprehensive data profile
  - `count_services()`: Count number of subscribed services per customer
  - `detect_outliers_iqr()`: Identify outliers using IQR method

- **List Comprehension:**
  - Dynamically collect service-related column names
  - Filter columns based on conditions

- **Additional Features:**
  - `FamilyFlag`: Boolean indicator for Partner or Dependents
  - `ServiceCount`: Total number of services subscribed

### 4. Descriptive Statistics
- Summary statistics for numeric variables (tenure, charges, service count)
- Frequency distributions for categorical variables (Contract, Internet, Payment)
- Churn rate calculations by segments

### 5. Data Visualization

**Univariate Analysis:**
- Distribution plots (histograms/KDE) for tenure, MonthlyCharges, TotalCharges
- Bar charts for categorical variables (Churn, Contract, InternetService)

**Bivariate Analysis:**
- Violin plots: Charges and tenure by Churn status
- Grouped bar charts: Churn rate by Contract, TenureGroup, Internet Service

**Multivariate Analysis:**
- Correlation heatmap (including ChurnFlag)
- Multi-level groupby visualizations

### 6. Statistical Testing
- **T-test:** Compare MonthlyCharges between churned and retained customers
- **Chi-square test:** Test association between Contract type and Churn
- Interpret p-values and statistical significance

### 7. Advanced Analysis
- **PCA (Principal Component Analysis):** Explore dimensionality and patterns in numeric features
- **Correlation Analysis:** Identify key drivers of churn

### 8. Group Analysis
- Aggregate churn rate and metrics by Contract type
- Multi-level grouping: InternetService × Contract
- Segment comparison: Identify high-risk customer profiles

## Key Findings

### Overall Churn Rate: **26.5%**

### Top Churn Drivers:

1. **Contract Type (Strongest Predictor)**
   - Month-to-month: **42% churn rate** ❌
   - One year: **11% churn rate** ⚠️
   - Two year: **3% churn rate** ✅
   - *Insight:* 14× higher churn for month-to-month vs two-year contracts

2. **Tenure**
   - Negative correlation with churn: **-0.35**
   - Churned customers: median tenure ~10 months
   - Retained customers: median tenure ~38 months
   - *Insight:* New customers (<12 months) are highest risk

3. **Monthly Charges**
   - Positive correlation with churn: **+0.19**
   - Churned customers: median ~$80/month
   - Retained customers: median ~$65/month
   - *Statistical significance:* T-test p-value < 0.001

4. **Internet Service Type**
   - Fiber optic: **42% churn** (month-to-month contracts)
   - DSL: **20% churn** (month-to-month contracts)
   - No internet: **7% churn**
   - *Insight:* Fiber optic pricing/quality issues detected

5. **Payment Method**
   - Electronic check: **~45% churn**
   - Automatic payment methods: Lower churn
   - *Insight:* Payment convenience reduces churn

## Business Recommendations

### Immediate Actions:
1. **Promote Long-Term Contracts**
   - Offer incentives for annual/multi-year contract upgrades
   - Create loyalty discounts for contract renewals
   - Target: Reduce month-to-month proportion from 55% to <40%

2. **Early Customer Retention Program**
   - Implement onboarding programs for new customers (0-12 months tenure)
   - Proactive outreach at 3, 6, and 12 month milestones
   - Special retention offers for high-bill, short-tenure customers

3. **Review Fiber Optic Strategy**
   - Reassess Fiber optic pricing (currently ~$90/month average)
   - Investigate service quality issues (higher churn despite premium service)
   - Consider competitive analysis vs market rates

4. **Payment Method Optimization**
   - Encourage autopay enrollment with incentives ($5/month discount)
   - Simplify payment processes for electronic check users
   - Target: Shift 20% of electronic check users to automatic payments

### Strategic Initiatives:
5. **Predictive Churn Modeling**
   - Build machine learning model (logistic regression, random forest)
   - Generate churn risk scores for proactive intervention
   - Automate high-risk customer identification

6. **Segmented Marketing Campaigns**
   - High-risk segment: Month-to-month + Fiber + <12 months tenure
   - Mid-risk segment: One-year contracts approaching renewal
   - Retention segment: Long-tenure customers (reward loyalty)

## How to Run the Analysis

### Step 1: Setup Environment
```bash
# Clone or download project files
cd path/to/project

# Install dependencies
pip install pandas numpy matplotlib seaborn scipy scikit-learn

# Ensure dataset is in the same directory
```

### Step 2: Open Jupyter Notebook
```bash
# Start Jupyter
jupyter notebook "New Pythond Project.ipynb"

# Or use VS Code with Jupyter extension
code "New Pythond Project.ipynb"
```

### Step 3: Run All Cells
- Execute cells sequentially from top to bottom
- Review outputs, visualizations, and insights
- All visualizations are generated inline

### Step 4: Export Results (Optional)
```python
# Export key visualizations as PNG
import matplotlib.pyplot as plt

# After generating each plot:
plt.savefig('churn_by_contract.png', dpi=300, bbox_inches='tight')
```

## Technical Highlights

### Advanced Python Techniques:
- ✅ Lambda functions for data transformation
- ✅ User-defined functions (UDFs) for reusable analysis
- ✅ List comprehensions for efficient data processing
- ✅ Pandas groupby and aggregation
- ✅ Statistical hypothesis testing (t-test, chi-square)
- ✅ Principal Component Analysis (PCA)
- ✅ Professional data visualization with Seaborn/Matplotlib

### Best Practices:
- Clean, well-documented code with markdown explanations
- Reproducible analysis workflow
- Clear section structure (Import → Clean → Engineer → Analyze → Conclude)
- Business-oriented insights and recommendations

## Results Summary

### Statistical Validation:
- **T-test (MonthlyCharges):** p < 0.001 ✅ Statistically significant difference
- **Chi-square (Contract × Churn):** p < 0.001 ✅ Strong association confirmed
- **PCA Variance Explained:** ~65% in first 2 components

### Model Readiness:
The data is clean, features are engineered, and exploratory insights confirm that predictive modeling would be highly effective. Recommended next step: Build classification model with 80/20 train-test split.

## Next Steps

1. **Predictive Modeling:** Implement logistic regression, random forest, or XGBoost
2. **A/B Testing:** Test retention interventions on high-risk segments
3. **Dashboard Development:** Create interactive Tableau/Power BI dashboard
4. **Additional Data Collection:** Customer satisfaction scores, service issues, competitor data
5. **Longitudinal Analysis:** Track churn trends over time

## Authors & Acknowledgments

**Project Type:** MTech Python EDA Group Project

**Date:** March 2026

**Dataset Source:** Telco Customer Churn (IBM Sample Dataset)

## License

This project is for educational purposes.

## Contact

For questions or feedback about this analysis, please contact the project team.

---

**Last Updated:** March 7, 2026
