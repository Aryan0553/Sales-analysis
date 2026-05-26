# 📊 Sales Performance Dashboard – Power BI

## 📌 Project Overview
This project focuses on analyzing retail sales data and building an interactive **Power BI dashboard** to gain insights into revenue, sales trends, customer behavior, and product performance.  
The dataset is cleaned, modeled, and visualized to support business decision-making.

---

## 🎯 Objectives
- Analyze total revenue and units sold
- Track monthly and yearly sales trends
- Compare performance across categories, countries, and sales channels
- Create an interactive dashboard using slicers

---


## 🛠 Tools & Technologies
- **Power BI Desktop**
- **Python (Pandas)** – Data Cleaning
- **DAX** – Measures & Calculations
- **CSV Dataset**

---

## 📂 Dataset
**File:** `final_cleaned_sales_data.csv`  
**Records:** 30,000  
**Columns:** 18  

Key columns:
- `order_date`
- `category`
- `country`
- `sales_channel`
- `units_sold`
- `revenue_usd`
- `discount_percent`
- `customer_rating`

---

## 🧹 Data Cleaning (Python)
```python
import pandas as pd

df = pd.read_csv("sales_data.csv")

# Remove duplicates
df = df.drop_duplicates()

# Convert date
df['order_date'] = pd.to_datetime(df['order_date'], errors='coerce')

# Numeric conversion
numeric_cols = [
    'base_price_usd','discount_percent',
    'final_price_usd','units_sold',
    'revenue_usd','customer_rating'
]
df[numeric_cols] = df[numeric_cols].apply(pd.to_numeric, errors='coerce')

# Logical validation
df = df[df['units_sold'] > 0]
df = df[df['final_price_usd'] <= df['base_price_usd']]

# Recalculate revenue
df['revenue_usd'] = df['final_price_usd'] * df['units_sold']

# Save cleaned file
df.to_csv("final_cleaned_sales_data.csv", index=False)
