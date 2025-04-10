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

-- 🔍 1. View the entire data
SELECT * 
FROM `airbnb-nyc-456311.sample_dataset.airbnb_listings`;

-- 🔢 2. Count total number of rows
SELECT COUNT(*) AS total_rows
FROM `airbnb-nyc-456311.sample_dataset.airbnb_listings`;

-- 🧾 3. List all column names in the table
SELECT column_name
FROM `airbnb-nyc-456311.sample_dataset.INFORMATION_SCHEMA.COLUMNS`
WHERE LOWER(table_name) = 'airbnb_listings';

-- 💰 4. Price per room type (raw view)
SELECT room_type, price 
FROM `airbnb-nyc-456311.sample_dataset.airbnb_listings`
WHERE room_type IS NOT NULL
ORDER BY room_type, price;

-- 💸 5. Average price per room type
SELECT room_type, 
       ROUND(AVG(price), 2) AS avg_price
FROM `airbnb-nyc-456311.sample_dataset.airbnb_listings`
WHERE room_type IS NOT NULL
GROUP BY room_type
ORDER BY avg_price DESC;

-- 💎 6. Top 3 most expensive room types with min and max price
SELECT room_type, 
       ROUND(AVG(price), 2) AS avg_price,
       MIN(price) AS min_price,
       MAX(price) AS max_price
FROM `airbnb-nyc-456311.sample_dataset.airbnb_listings`
WHERE room_type IS NOT NULL
GROUP BY room_type
ORDER BY avg_price DESC
LIMIT 3;

-- ⚠️ 7. Hosts offering ₹0 listings in top 3 most expensive room types
SELECT host_id,
       host_name,
       name AS listing_name,
       room_type, 
       price
FROM `airbnb-nyc-456311.sample_dataset.airbnb_listings`
WHERE price = 0
  AND room_type IN (
    SELECT room_type
    FROM `airbnb-nyc-456311.sample_dataset.airbnb_listings`
    WHERE room_type IS NOT NULL
    GROUP BY room_type
    ORDER BY AVG(price) DESC
    LIMIT 3
  )
ORDER BY room_type, host_name;

-- 🌟 8. Listings with highest number of reviews
SELECT name AS listing_name,
       number_of_reviews,
       reviews_per_month
FROM `airbnb-nyc-456311.sample_dataset.airbnb_listings`
ORDER BY number_of_reviews DESC,
         reviews_per_month DESC
LIMIT 20;

-- 📉 9. Are highly-reviewed listings also low-priced?
SELECT name AS listing_name,
       number_of_reviews,
       reviews_per_month,
       price
FROM `airbnb-nyc-456311.sample_dataset.airbnb_listings`
ORDER BY number_of_reviews DESC,
         reviews_per_month DESC
LIMIT 20;
