# 🚗 BMW Worldwide Sales Analytics Dashboard

This repository contains a **Power BI Dashboard** built on BMW's global sales dataset (2010-2024). The dashboard provides **interactive insights** into BMW's worldwide sales performance, revenue trends, regional distribution, and model rankings across 50,000+ transactions.

![Demo](https://github.com/user-attachments/assets/6c2fa386-b755-4d2a-b982-1123c1bd35d6)

## 📑 Dataset

**📊 Source**: [BMW Worldwide Sales Records (2010–2024)](https://www.kaggle.com/datasets/ahmadrazakashif/bmw-worldwide-sales-records-20102024)

**🌍 Coverage**:
- **Period**: January 2010 - December 2024 (15 years)
- **Records**: 50,000+ individual sales transactions
- **Regions**: Asia, Europe, North America, Middle East, South America, Africa
- **Models**: 10+ BMW vehicle lines (3 Series, 5 Series, 7 Series, X1, X3, X5, X6, M3, M5, i3, i8)

**📋 Dataset Attributes**:
- Model, Year, Region, Color
- Fuel Type (Petrol, Diesel, Electric, Hybrid)
- Transmission (Manual, Automatic)
- Engine Size (Liters), Mileage (KM)
- Price (USD), Sales Volume
- Sales Classification (High/Low)

## 📂 Project Structure

* **🏠 HOME Page** → Executive summary with key KPIs, revenue trends, and dashboard introduction.
* **💰 REVENUE Page** → Deep-dive financial analytics with revenue by year, region, model, and fuel type.
* **🏆 RANKING Page** → Performance leaderboards showcasing top models, revenue rankings, and market leaders.

## 🧮 DAX Measures Used

Here are the main **DAX measures** created for calculations:

### **Core Metrics**

```DAX
Total Revenue = SUM('BMW_Sales_Data'[Price_USD])
```

```DAX
Total Sales Volume = SUM('BMW_Sales_Data'[Sales_Volume])
```

```DAX
Total Orders = COUNTROWS('BMW_Sales_Data')
```

```DAX
Average Transaction Price = 
DIVIDE(
    SUM('BMW_Sales_Data'[Price_USD]),
    SUM('BMW_Sales_Data'[Sales_Volume]),
    0
)
```

```DAX
High Sales Count = 
CALCULATE(
    COUNTROWS('BMW_Sales_Data'),
    'BMW_Sales_Data'[Sales_Classification] = "High"
)
```

### **TOP 3 Performance Metrics**

```DAX
Revenue TOP 3 = 
VAR TopModels = 
    TOPN(
        3,
        SUMMARIZE(
            'BMW_Sales_Data',
            'BMW_Sales_Data'[Model],
            "Revenue", SUM('BMW_Sales_Data'[Price_USD])
        ),
        [Revenue],
        DESC
    )
RETURN
    SUMX(TopModels, [Revenue])
```

```DAX
Orders TOP 3 = 
VAR TopModels = 
    TOPN(
        3,
        SUMMARIZE(
            'BMW_Sales_Data',
            'BMW_Sales_Data'[Model],
            "TotalOrders", SUM('BMW_Sales_Data'[Sales_Volume])
        ),
        [TotalOrders],
        DESC
    )
RETURN
    SUMX(TopModels, [TotalOrders])
```

```DAX
ATP TOP 3 = 
VAR TopModels = 
    TOPN(
        3,
        SUMMARIZE(
            'BMW_Sales_Data',
            'BMW_Sales_Data'[Model],
            "Revenue", SUM('BMW_Sales_Data'[Price_USD]),
            "Volume", SUM('BMW_Sales_Data'[Sales_Volume])
        ),
        [Revenue],
        DESC
    )
VAR TotalRevenue = SUMX(TopModels, [Revenue])
VAR TotalVolume = SUMX(TopModels, [Volume])
RETURN
    DIVIDE(TotalRevenue, TotalVolume, 0)
```

```DAX
Sales Volume TOP 3 = 
VAR TopModels = 
    TOPN(
        3,
        SUMMARIZE(
            'BMW_Sales_Data',
            'BMW_Sales_Data'[Model],
            "Volume", SUM('BMW_Sales_Data'[Sales_Volume])
        ),
        [Volume],
        DESC
    )
RETURN
    SUMX(TopModels, [Volume])
```

### **Top Performer Identification**

```DAX
Top Model Name = 
VAR TopModel = 
    TOPN(
        1,
        SUMMARIZE(
            'BMW_Sales_Data',
            'BMW_Sales_Data'[Model],
            "Revenue", SUM('BMW_Sales_Data'[Price_USD])
        ),
        [Revenue],
        DESC
    )
RETURN
    MAXX(TopModel, 'BMW_Sales_Data'[Model])
```

```DAX
Top Model Revenue = 
VAR TopModel = 
    TOPN(
        1,
        SUMMARIZE(
            'BMW_Sales_Data',
            'BMW_Sales_Data'[Model],
            "Revenue", SUM('BMW_Sales_Data'[Price_USD])
        ),
        [Revenue],
        DESC
    )
RETURN
    SUMX(TopModel, [Revenue])
```

```DAX
Top Model Volume = 
VAR TopModel = [Top Model Name]
RETURN
    CALCULATE(
        SUM('BMW_Sales_Data'[Sales_Volume]),
        'BMW_Sales_Data'[Model] = TopModel
    )
```

### **Ranking & Market Share**

```DAX
Revenue % of Total = 
DIVIDE(
    SUM('BMW_Sales_Data'[Price_USD]),
    CALCULATE(
        SUM('BMW_Sales_Data'[Price_USD]),
        ALL('BMW_Sales_Data'[Model])
    ),
    0
)
```

```DAX
Market Share % = 
DIVIDE(
    [Total Revenue],
    CALCULATE([Total Revenue], ALL('BMW_Sales_Data'[Model])),
    0
)
```

### **Year-over-Year Growth**

```DAX
Revenue PY = 
CALCULATE(
    [Total Revenue],
    SAMEPERIODLASTYEAR('BMW_Sales_Data'[Date])
)
```

```DAX
Revenue Growth % = 
DIVIDE(
    [Total Revenue] - [Revenue PY],
    [Revenue PY],
    0
)
```

### **Budget Analysis**

```DAX
Budget Target = [Total Revenue] * 1.15
```

```DAX
High Sales % = 
DIVIDE(
    [High Sales Count],
    [Total Orders],
    0
)
```

## 📸 Dashboard Screenshots

### 🏠 HOME Page
<img width="1424" height="798" alt="Screenshot 2025-10-27 182556" src="https://github.com/user-attachments/assets/37ab0552-4c35-4ad7-8b34-4af1634c540a" />

**Features**:
- Welcome banner with dashboard description
- Key KPIs: Total Revenue, Total Orders, Average Transaction Price
- Year slicer for filtering
- Revenue trend visualization
- Navigation to detailed pages



### 💰 REVENUE Page
<img width="1423" height="800" alt="Screenshot 2025-10-27 182607" src="https://github.com/user-attachments/assets/718e0419-e298-453f-9be7-11029019eae4" />

**Features**:
- Revenue and Sales Volume by Year (Clustered Column Chart)
- Revenue vs Budget Gauge (88.6% achievement)
- Revenue by Region (Donut Chart with percentages)
- Revenue by Model (Horizontal Bar Chart)
- Revenue by Fuel Type (Donut Chart)
- Top Performers Table with conditional formatting



### 🏆 RANKING Page
<img width="1423" height="798" alt="Screenshot 2025-10-27 182615" src="https://github.com/user-attachments/assets/01e87a38-6487-4053-abd7-7497bd78b79f" />

**Features**:
- Top 3 KPI Cards: Revenue, Orders, ATP, Sales Volume
- Best Performer Callout (dynamic text highlighting top model)
- Ranking Table with Gold/Silver/Bronze highlighting
- Model Performance Matrix (Model × Year heat map)
- Competitive leaderboard with data bars


## 🎨 Theme

* **Dark premium theme** with modern aesthetics
* **Color palette**:
  - Primary: `#6C5CE7` (Purple) - Premium/BMW Brand
  - Success: `#00B894` (Green) - Growth/Performance
  - Warning: `#FDCB6E` (Gold) - Excellence/Rankings
  - Info: `#74B9FF` (Blue) - Scale/Volume
  - Background: `#0F1419` (Dark) - Professional look
* **Consistent styling**: Card designs, borders with border-radius, gradient effects
* **Typography**: Segoe UI family with hierarchical sizing

### Theme JSON
Custom Power BI theme file included: `Theme.json`

## 🚀 Features

* **Interactive slicers** synced across all pages:
  - Year filter (2010-2024)
  - Region selector (Asia, Europe, North America, Middle East, South America, Africa)
  - Model selector
  - Sales Classification filter
* **Navigation system** with HOME, REVENUE, RANKING buttons
* **Top 3 Analysis** across multiple dimensions
* **Conditional formatting**:
  - Data bars on revenue columns
  - Heat maps in matrix visuals
  - Gold/Silver/Bronze row highlighting for top 3
* **KPIs**: Total Revenue, Orders, ATP, Sales Volume
* **Comparative analysis**: 
  - Revenue vs Budget
  - Regional distribution
  - Model performance over time
  - Fuel type preferences by market

## 📈 Key Insights

### 🌍 **Regional Performance**
* **Asia** leads in sales volume, demonstrating BMW's strong foothold in the world's fastest-growing market
* **Europe** maintains steady premium positioning with consistent high ATP
* **North America** shows balanced performance across all model categories

### 🚗 **Model Analysis**
* **5 Series** dominates revenue generation across multiple regions
* **X-Series SUVs** (X3, X5, X6) show strong market penetration in Middle East and North America
* **M-Series** maintains premium positioning with highest average transaction prices
* **i-Series** (electric) gaining momentum in sustainability-focused markets

### ⚡ **Fuel Type Trends**
* **Electric and Hybrid** vehicles now account for significant percentage of sales, up from minimal presence in 2010
* **Diesel** remains popular in European markets
* **Petrol** engines dominate in Middle Eastern markets
* Clear shift toward sustainable powertrains over the 15-year period

### 💰 **Pricing Insights**
* Average transaction price: **$85,000 - $95,000** (varies by year and model)
* Top 3 models contribute to **~65%** of total revenue
* High sales classification correlates with premium models and newer years
* Clear premium positioning maintained across all regions

### 📊 **Sales Classification**
* **"High" sales** transactions average **7,500+ units** per transaction
* Geographic concentration of high-value sales in Asia and Europe
* Correlation between newer models and high sales classification
