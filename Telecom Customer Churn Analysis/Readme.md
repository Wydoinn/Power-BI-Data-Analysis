# 📞 Telecom Customer Churn Analysis Dashboard

A comprehensive Power BI dashboard analyzing customer churn patterns in the telecommunications industry, providing actionable insights for customer retention strategies.


![Demo](https://github.com/user-attachments/assets/23de14dd-ff5a-4b87-a832-50177ae368b2)


## 📊 Project Overview

Customer churn is a critical challenge in telecommunications, where retaining existing customers is significantly more cost-effective than acquiring new ones. This project analyzes customer behavior patterns, identifies churn drivers, and provides strategic recommendations for improving customer retention.

### 🎯 Key Objectives
- Predict customer churn likelihood using behavioral patterns
- Identify high-risk customer segments
- Analyze financial impact of customer churn
- Develop data-driven retention strategies

## 📈 Dashboard Pages

### 1. Executive Summary (High-Level KPIs)
**Purpose**: Provides C-level executives with key performance indicators at a glance

**Key Metrics**:
- Total Customers: 7,043
- Overall Churn Rate: 26.5%
- Average Monthly Charges: $64.76
- Revenue Lost from Churned Customers

**Visualizations**:
- KPI Cards for critical metrics
- Donut Chart showing churn distribution
- Column Chart comparing churn by senior citizen status
- Line Chart displaying churn rate trends by tenure

### 2. Churn Drivers Analysis
**Purpose**: Deep dive into why customers are leaving

**Key Insights**:
- Month-to-month contracts have the highest churn rate (42.7%)
- Fiber optic internet users churn more than DSL users
- Electronic check payment method shows highest churn
- Early tenure customers (<12 months) are at highest risk

**Visualizations**:
- Stacked Column Charts by contract type and internet service
- Matrix heatmap for paperless billing vs churn
- Scatterplot showing tenure vs monthly charges relationship

### 3. Financial Insights & Retention Strategy
**Purpose**: Quantify financial impact and model retention improvements

**Key Features**:
- Revenue comparison: Retained vs Lost customers
- Average Lifetime Value analysis
- What-if scenario modeling for retention improvements
- ROI projections for retention initiatives

**Interactive Elements**:
- What-if parameter slider for retention improvement scenarios
- Waterfall chart showing revenue impact by customer segments

### 4. Customer Segmentation & Risk Analysis
**Purpose**: Identify high-risk customer segments for targeted interventions

**Segmentation Criteria**:
- Tenure buckets (0-12, 13-24, 25-48, 49+ months)
- Monthly charges ranges
- Service combinations
- Contract types

### 5. Service Usage vs Churn
**Purpose**: Analyze correlation between service adoption and churn

**Key Findings**:
- Customers without online security services show higher churn
- Lack of tech support correlates with increased churn risk
- Streaming service adoption patterns vary by churn status

### 6. Tenure & Billing Patterns
**Purpose**: Understand customer lifecycle and payment behavior impact

**Analysis Areas**:
- Churn rate decline over customer tenure
- Payment method preferences by customer segments
- Total charges distribution analysis

### 7. Predictive Indicators & What-If Analysis
**Purpose**: Highlight top churn predictors and simulate intervention scenarios

**Predictive Features**:
- Contract type (strongest predictor)
- Internet service type
- Payment method
- Service adoption score
- Customer tenure

## 🔧 Technical Implementation

### Data Preparation (Power Query)
```powerquery
// Convert TotalCharges to numeric
= Table.TransformColumnTypes(Source, {{"TotalCharges", type number}})

// Create tenure buckets
= Table.AddColumn(#"Previous Step", "TenureBucket", 
    each if [tenure] <= 12 then "0-12" 
    else if [tenure] <= 24 then "13-24" 
    else if [tenure] <= 48 then "25-48" 
    else "49+")

// Clean service columns
= Table.ReplaceValue(#"Previous Step", "No internet service", "No", 
    Replacer.ReplaceText, {"OnlineSecurity", "OnlineBackup", "DeviceProtection"})
```

### Key DAX Measures

```dax
// Churn Rate Calculation
Churn Rate % = DIVIDE([Churned Customers], [Total Customers], 0)

// Revenue Lost from Churn
Revenue Lost = CALCULATE(SUM(Customers[TotalCharges]), Customers[Churn] = "Yes")

// Service Risk Score
ServiceScore = 
IF(Customers[OnlineSecurity]="No",1,0) + 
IF(Customers[OnlineBackup]="No",1,0) + 
IF(Customers[DeviceProtection]="No",1,0) + 
IF(Customers[TechSupport]="No",1,0)

// Projected Revenue (What-If Analysis)
Projected Revenue = [Revenue Retained] + ([Revenue Lost] * ('Retention Improvement %'[Value]/100))
```

## 📊 Dataset Information

**Source**: [Telcom Customer Churn Dataset](https://www.kaggle.com/datasets/mosapabdelghany/telcom-customer-churn-dataset) - Kaggle
**Author**: Mosa Abdelghany
- **Rows**: 7,043 customers
- **Columns**: 21 features
- **Target Variable**: Churn (Yes/No)
- **File Format**: CSV
- **License**: Open Dataset

### Key Features:
- **Demographics**: Gender, Senior Citizen status, Partner, Dependents
- **Account Info**: Tenure, Contract type, Payment method, Billing preferences
- **Services**: Phone, Internet, Security, Backup, Streaming services
- **Financial**: Monthly charges, Total charges

## 🎨 Design & Visualization

### Custom Theme: "Plexus Theme"
A professionally crafted Power BI theme with a modern, clean aesthetic designed specifically for this dashboard.

**Color Palette:**
- **Primary Data Colors**: Golden (#FFD700), Coral (#F2A140), Pink (#D94A8C), Purple gradient (#8A4E9E), Blue spectrum (#4A78D9)
- **Background**: Light (#F8F9FD) for excellent readability
- **Text Colors**: 
  - Headers: Dark slate (#2D2D4A)
  - Labels: Medium gray (#4A4A6B)
  - Secondary text: Light gray (#6B6B8A)
- **Accent Color**: Pink (#D94A8C) for highlights and table accents

### Visual Styling Features:
- **Drop shadows** for depth and professional appearance
- **Consistent typography** using Segoe UI font family
- **Hover effects** on interactive elements
- **Gradient color schemes** for enhanced visual appeal
- **High contrast ratios** for accessibility compliance

### Interactive Features:
- Dynamic slicers for real-time filtering
- What-if parameters for scenario planning
- Drill-through capabilities between pages
- Cross-filtering across all visuals

## 📸 Dashboard Screenshots

### Executive Summary (High-Level KPIs)
<img width="1433" height="806" alt="Screenshot 2025-09-28 111053" src="https://github.com/user-attachments/assets/bd84eee5-da47-460c-8558-f8693e53968f" />

### Churn Drivers Analysis
<img width="1439" height="798" alt="Screenshot 2025-09-28 111106" src="https://github.com/user-attachments/assets/4d7f0e4b-ea32-4c59-a8a3-deb04f455dd8" />

### Financial Insights & Retention Strategy
<img width="1436" height="801" alt="Screenshot 2025-09-28 111118" src="https://github.com/user-attachments/assets/ef783745-9fde-4258-a6e5-8c4b7df6b44c" />

### Customer Segmentation & Risk Analysis
<img width="1436" height="798" alt="Screenshot 2025-09-28 111132" src="https://github.com/user-attachments/assets/32556cc8-e02e-4c57-90df-f0e9ab783067" />

### Service Usage vs Churn
<img width="1437" height="803" alt="Screenshot 2025-09-28 111149" src="https://github.com/user-attachments/assets/86da5670-d1a6-4b47-85c7-24c94895ad31" />

### Tenure & Billing Patterns
<img width="1437" height="805" alt="Screenshot 2025-09-28 111202" src="https://github.com/user-attachments/assets/399176e0-48c2-4433-a90e-a63fd025e3cb" />

### Predictive Indicators & What-If Analysis
<img width="1439" height="803" alt="Screenshot 2025-09-28 111215" src="https://github.com/user-attachments/assets/24e44883-1a5a-46d2-a6de-3eddec8ceb06" />


## 🔍 Key Business Insights

### 1. Contract Type Impact
- **Month-to-month**: 42.7% churn rate (3,875 customers)
- **One-year**: 11.3% churn rate (1,473 customers)  
- **Two-year**: 2.8% churn rate (1,695 customers)
- **Strategic Finding**: Longer contract commitments reduce churn by up to 93%

### 2. Tenure Patterns & Customer Lifecycle
- **Critical period**: 0-12 months (47.4% churn rate - highest vulnerability)
- **Improvement phase**: 13-24 months (35.2% churn rate)
- **Stabilization**: 25-48 months (15.6% churn rate) 
- **Loyalty segment**: 49+ months (6.4% churn rate)
- **Key Finding**: Customer retention dramatically improves after the 12-month milestone

### 3. Payment Method Risk Assessment
- **Electronic check**: 45.3% churn rate (highest risk payment method)
- **Mailed check**: 19.1% churn rate
- **Bank transfer (automatic)**: 16.2% churn rate
- **Credit card (automatic)**: 15.2% churn rate (most secure payment method)
- **Strategic Insight**: Automatic payment methods reduce churn by 66% compared to electronic checks

### 4. Service Bundle Dependencies & Add-on Impact
- **Internet Service Analysis**:
  - Fiber optic customers: 30.9% churn rate
  - DSL customers: 18.8% churn rate
  - No internet service: 7.4% churn rate
- **Security Services Impact**:
  - Without online security: 41.8% churn rate
  - With online security: 14.6% churn rate (65% churn reduction)
- **Tech Support Correlation**:
  - Without tech support: 41.7% churn rate  
  - With tech support: 15.2% churn rate (64% churn reduction)
- **Service Bundle Finding**: Customers with 3+ additional services show 58% lower churn rates

### 5. Demographics & Customer Profile Analysis
- **Senior Citizens**: 41.7% churn rate (significantly higher than average)
- **Non-senior citizens**: 23.6% churn rate
- **Gender Impact**: Minimal difference (Female: 26.9%, Male: 26.2%)
- **Family Structure**: 
  - Without partners: 33.0% churn rate
  - With partners: 19.7% churn rate
  - With dependents: 15.5% churn rate (family stability reduces churn)

### 6. Financial Behavior Patterns
- **High-value customers** (>$80 monthly): 32.1% churn rate
- **Mid-tier customers** ($40-80 monthly): 18.3% churn rate  
- **Budget customers** (<$40 monthly): 9.2% churn rate
- **Paperless billing**: 33.6% churn rate vs 16.4% for traditional billing
- **Revenue Impact**: $2.9M annual revenue at risk from churned customers

### 7. Service Utilization & Streaming Patterns
- **Streaming TV**: 
  - With service: 28.5% churn rate
  - Without service: 21.3% churn rate
- **Streaming Movies**: Similar pattern to TV streaming
- **Multiple Lines**:
  - Single line: 25.5% churn rate
  - Multiple lines: 18.4% churn rate
- **Phone Service**: 90.3% of all customers have phone service (minimal churn impact)
