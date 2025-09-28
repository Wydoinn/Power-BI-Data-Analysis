# 📞 Telecom Customer Churn Analysis Dashboard

A comprehensive Power BI dashboard analyzing customer churn patterns in the telecommunications industry, providing actionable insights for customer retention strategies.

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

## 🔍 Key Business Insights

### 1. Contract Type Impact
- **Month-to-month**: 42.7% churn rate
- **One-year**: 11.3% churn rate
- **Two-year**: 2.8% churn rate

### 2. Service Dependencies
- Customers with comprehensive service packages show 23% lower churn
- Tech support adoption reduces churn by 15%
- Online security services correlate with higher retention

### 3. Payment Method Risk
- Electronic check: Highest churn risk
- Credit card (automatic): Lowest churn risk
- Bank transfer: Moderate risk

### 4. Tenure Patterns
- Critical period: First 12 months (highest churn risk)
- Stability threshold: 24+ months (significant churn reduction)
- Loyalty segment: 48+ months (minimal churn)


## 🛠️ Tools & Technologies

- **Power BI Desktop**: Dashboard development and visualization
- **Custom Theme**: "Plexus Theme" - professionally designed color palette and styling
- **Power Query**: Data transformation and preparation
- **DAX**: Advanced calculations and measures
- **Excel**: Initial data exploration and validation
