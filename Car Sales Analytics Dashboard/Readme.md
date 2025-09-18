# 🚗 Car Sales Analytics Dashboard

This repository contains a **Power BI Dashboard** built on a second-hand car sales dataset. The dashboard provides **interactive insights** into car sales trends, pricing, performance, and fuel type distribution.

📊 **Dataset**: [Car Sales Dataset (Kaggle)](https://www.kaggle.com/datasets/msnbehdani/mock-dataset-of-second-hand-car-sales)


## 📂 Project Structure

* **Home Page** → Navigation hub with global slicers (Year, Price, Manufacturer, Model, Fuel Type).
* **Overview Page** → High-level KPIs & sales trends by manufacturer and model.
* **Pricing Page** → Price analysis by engine size, manufacturer, and car age.
* **Performance Page** → Fuel type analysis with average prices, counts, and distribution.
* **Drillthrough Page** → Row-level details for a selected car model/manufacturer.


## 🧮 DAX Measures Used

Here are the main **DAX measures** created for calculations:

```DAX
Total Cars = COUNTROWS(car_sales_data)
```

```DAX
Average Price = AVERAGE(car_sales_data[Price])
```

```DAX
Average Mileage = AVERAGE(car_sales_data[Mileage])
```

```DAX
Average Age = AVERAGE(car_sales_data[Car Age])
```

```DAX
Avg Engine Size = AVERAGE(car_sales_data[Engine size])
```

```DAX
Median Price = MEDIAN(car_sales_data[Price])
```

```DAX
Price per KM = DIVIDE([Average Price], [Average Mileage])
```

```DAX
% of Sales = DIVIDE([Total Cars], CALCULATE([Total Cars], ALL(car_sales_data)))
```

```DAX
-- Most Common Year
Most Common Year =
VAR SummaryTable =
    SUMMARIZE(
        car_sales_data,
        car_sales_data[Year of manufacture],
        "CountRows", COUNTROWS(car_sales_data)
    )
RETURN
    MAXX(
        TOPN(1, SummaryTable, [CountRows], DESC),
        car_sales_data[Year of manufacture]
    )
```

```DAX
-- Most Common Fuel Type
Most Common Fuel Type =
VAR SummaryTable =
    SUMMARIZE(
        car_sales_data,
        car_sales_data[Fuel type],
        "CountRows", COUNTROWS(car_sales_data)
    )
RETURN
    MAXX(
        TOPN(1, SummaryTable, [CountRows], DESC),
        car_sales_data[Fuel type]
    )
```

```DAX
-- YoY %
YoY % =
DIVIDE(
    [Average Price] - [Avg Price Prev Year],
    [Avg Price Prev Year]
)

Avg Price Prev Year =
CALCULATE(
    [Average Price],
    DATEADD(YearTable[Year], -1, YEAR)
)
```


## 📸 Dashboard Screenshots

### 🏠 Home Page

![Home Page](./screenshots/home.png)

### 📊 Overview Page

![Overview](./screenshots/overview.png)

### 💰 Pricing Page

![Pricing](./screenshots/pricing.png)

### 🔧 Performance Page

![Performance](./screenshots/performance.png)

### 🔍 Drillthrough Page

![Drillthrough](./screenshots/drillthrough.png)


## 🎨 Theme

* **Purple theme** implemented in **light mode**.
* Consistent slicer styling and KPI card design.



## 🚀 Features

* **Interactive slicers** synced across pages.
* **Clear all slicers button** on home page.
* **Drillthrough analysis** for deep dive into specific models/manufacturers.
* **KPIs**: Total Cars, Avg Price, Avg Mileage, Avg Age.
* **Comparative analysis**: Price vs Age, Price vs Engine Size, Sales Distribution.


## 📌 How to Use

1. Download the dataset from Kaggle.
2. Open `Car_Sales_Analytics.pbix` in Power BI.
3. Refresh data source to load dataset.
4. Navigate using the **Home Page buttons**.
5. Apply slicers to interact with the report.
6. Right-click on visuals to **drillthrough** into model/manufacturer details.


## 📈 Insights

* Ford and VW dominate sales volume.
* Porsche has the **highest average price distribution**.
* Hybrid cars show **higher median pricing**.
* Clear depreciation trend: **older cars = lower average prices**.
