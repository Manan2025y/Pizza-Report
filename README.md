
# 🍕 Project Overview  
**Project Title:** Pizza Sales Analysis  
**Level:** Beginner to Intermediate  
**Tools Used:** SQL Server / PostgreSQL, Power BI  
**Database:** `pizza_sales`

This project explores pizza sales data using SQL and Power BI. It demonstrates how data analysts use queries to calculate KPIs, identify sales trends, and uncover product performance insights. The analysis is visualized through interactive dashboards.

---

## 🎯 Objectives  
- **Database Setup:** Create and populate the pizza sales table.  
- **KPI Analysis:** Use SQL to calculate key performance indicators.  
- **Trend Analysis:** Explore daily and monthly order patterns.  
- **Category Insights:** Analyze sales by pizza category and size.  
- **Product Performance:** Identify top and bottom-performing pizzas.  
- **Visualization:** Build Power BI dashboards to present findings.

---

## 🗂️ Project Structure  

### 1. Database Setup  
```sql
CREATE TABLE pizza_sales (
    order_id INT,
    order_date DATE,
    pizza_name VARCHAR(100),
    pizza_category VARCHAR(50),
    pizza_size VARCHAR(20),
    quantity INT,
    unit_price DECIMAL(10,2),
    total_price DECIMAL(10,2)
);
```

### 2. Data Import  
```sql
COPY pizza_sales
FROM 'C:\data\pizza_sales.csv'
DELIMITER ','
CSV HEADER;
```

---

## 📊 SQL Analysis  

### A. KPI’s  
```sql
SELECT SUM(total_price) AS Total_Revenue FROM pizza_sales;
SELECT (SUM(total_price) / COUNT(DISTINCT order_id)) AS Avg_order_Value FROM pizza_sales;
SELECT SUM(quantity) AS Total_pizza_sold FROM pizza_sales;
SELECT COUNT(DISTINCT order_id) AS Total_Orders FROM pizza_sales;
SELECT CAST(CAST(SUM(quantity) AS DECIMAL(10,2)) /
CAST(COUNT(DISTINCT order_id) AS DECIMAL(10,2)) AS DECIMAL(10,2)) AS Avg_Pizzas_per_order FROM pizza_sales;
```

### B. Daily Trend for Orders  
```sql
SELECT DATENAME(DW, order_date) AS order_day, COUNT(DISTINCT order_id) AS total_orders
FROM pizza_sales
GROUP BY DATENAME(DW, order_date);
```

### C. Monthly Trend for Orders  
```sql
SELECT DATENAME(MONTH, order_date) AS Month_Name, COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
GROUP BY DATENAME(MONTH, order_date);
```

### D. % of Sales by Pizza Category  
```sql
SELECT pizza_category, CAST(SUM(total_price) AS DECIMAL(10,2)) AS total_revenue,
CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) FROM pizza_sales) AS DECIMAL(10,2)) AS PCT
FROM pizza_sales
GROUP BY pizza_category;
```

### E. % of Sales by Pizza Size  
```sql
SELECT pizza_size, CAST(SUM(total_price) AS DECIMAL(10,2)) AS total_revenue,
CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) FROM pizza_sales) AS DECIMAL(10,2)) AS PCT
FROM pizza_sales
GROUP BY pizza_size
ORDER BY pizza_size;
```

### F. Total Pizzas Sold by Category (Feb Only)  
```sql
SELECT pizza_category, SUM(quantity) AS Total_Quantity_Sold
FROM pizza_sales
WHERE MONTH(order_date) = 2
GROUP BY pizza_category
ORDER BY Total_Quantity_Sold DESC;
```

### G–L. Product Performance  
```sql
-- Top 5 Pizzas by Revenue
SELECT TOP 5 pizza_name, SUM(total_price) AS Total_Revenue
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Revenue DESC;

-- Bottom 5 Pizzas by Revenue
SELECT TOP 5 pizza_name, SUM(total_price) AS Total_Revenue
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Revenue ASC;

-- Top 5 Pizzas by Quantity Sold
SELECT TOP 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold DESC;

-- Bottom 5 Pizzas by Quantity Sold
SELECT TOP 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold ASC;

-- Top 5 Pizzas by Orders
SELECT TOP 5 pizza_name, COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Orders DESC;

-- Bottom 5 Pizzas by Orders
SELECT TOP 5 pizza_name, COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Orders ASC;
```

---

## 📈 Power BI Dashboards  

### 🧾 Dashboard 1: Pizza Sales Report  
**Highlights:**  
- KPI Summary: Avg Order Value ₹38.31, Total Orders 21.35K, Avg Pizzas per Order 2.32, Total Pizzas Sold 49.57K, Revenue ₹817.86K  
- Daily Trend: Highest orders on Friday and Saturday  
- Monthly Trend: Peak in July and October  
- Sales by Category: Classic pizzas lead with ₹411.9K  
- Sales by Size: Large pizzas dominate with ₹595.5K  

### 🍕 Dashboard 2: Product Performance Report  
**Highlights:**  
- Top 5 Pizzas by Revenue: The Chicken Pizza leads with ₹38K  
- Top 5 by Quantity: Chicken Supreme Pizza tops with 1.9K sold  
- Top 5 by Orders: Chicken Supreme Pizza again leads with 2.3K orders  
- Bottom 5 Pizzas: The Ice-Cream Pizza consistently ranks lowest across revenue, quantity, and orders  

---

## 🔍 Findings  

- **Revenue Distribution:** Classic and Supreme categories dominate sales  
- **Size Preference:** Large pizzas contribute the most to revenue  
- **Order Trends:** Weekends and mid-year months show peak activity  
- **Top Performers:** Chicken Supreme and The Chicken Pizza are bestsellers  
- **Low Performers:** Ice-Cream Pizza shows minimal engagement  

---

## 📄 Reports  

- **Sales Summary:** Revenue, order volume, and pizza size/category breakdown  
- **Trend Analysis:** Daily and monthly order patterns  
- **Product Insights:** Top and bottom pizzas by revenue, quantity, and orders  

---

## ✅ Conclusion  

This project offers a comprehensive look at pizza sales using SQL and Power BI. It highlights how data-driven decisions can improve product offerings, optimize pricing, and enhance customer satisfaction.

---

## 🚀 How to Use  

- **Clone the Repository:** Download from GitHub  
- **Initialize the Database:** Run SQL scripts to create and populate the pizza_sales table  
- **Explore with Power BI:** Connect to the database and build dashboards  
- **Customize & Extend:** Modify queries to explore new business questions  

---

**Author – Manan**  
This project is part of my personal portfolio, showcasing SQL and Power BI skills for data analytics. For feedback or collaboration, feel free to reach out.
