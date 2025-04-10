# airbnb_nyc_dataset
SQL-based Airbnb NYC data analysis using BigQuery
# 🏘️ Airbnb NYC Data Analysis (BigQuery + SQL)

This project explores Airbnb listing data for New York City using SQL in BigQuery. It covers pricing analysis, host behavior, and listing performance to uncover actionable business insights.

---

## 📂 Dataset Info

- **Project ID:** `airbnb-nyc-456311`
- **Dataset:** `sample_dataset`
- **Table:** `airbnb_listings`
- **Full Table Path:** `airbnb-nyc-456311.sample_dataset.airbnb_listings`

---

## 🧠 Analysis Overview

### 🔍 1. Basic Exploration
- View the entire dataset  
- Count total rows  
- List all column names  

### 💰 2. Pricing Insights by Room Type
- Price distribution for each room type  
- Average, minimum, and maximum price for each room type  
- Identify top 3 most expensive room types  

### ❗ 3. Zero-Priced Listings in Top Room Types
- Find hosts listing top-tier properties at ₹0  
- Potential opportunity for business optimization  

### 🌟 4. Review & Performance Insights
- Listings with the most reviews  
- Review count vs pricing  

---

## 📜 SQL Queries Used

### View Entire Table
```sql
SELECT * 
FROM `airbnb-nyc-456311.sample_dataset.airbnb_listings`;
