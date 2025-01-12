# Visulaization
This SQL script creates a sales table within a business database, inserts sample order data, and provides:  Order Counts by Category Daily Totals for Quantity and Sales Monthly Revenue by Category

#Creating Database , Schema And Table 
create database business;
create schema business.target;
-- Create the sales table
CREATE TABLE sales (
 order_id INTEGER,
 product_name VARCHAR(100),
 product_category VARCHAR(50),
 quantity INTEGER,
 price FLOAT,
 order_date DATE
);
#Insert Sample Data Into The Sales Table
INSERT INTO sales (order_id, product_name, product_category, quantity, price,
order_date) VALUES
 (1, 'Product A', 'Electronics', 10, 50.0, '2023-01-01'),
 (2, 'Product B', 'Clothing', 5, 75.0, '2023-01-02'),
 (3, 'Product C', 'Electronics', 8, 100.0, '2023-01-03'),
 (4, 'Product D', 'Furniture', 3, 150.0, '2023-01-04'),
 (5, 'Product E', 'Clothing', 6, 80.0, '2023-01-05');
 (6, 'Product F', 'Electronics', 12, 120.0, '2023-01-06'),
 (7, 'Product G', 'Furniture', 4, 200.0, '2023-01-07'),
 (8, 'Product H', 'Clothing', 7, 90.0, '2023-01-08'),
 (9, 'Product I', 'Electronics', 15, 110.0, '2023-01-09'),
 (10, 'Product J', 'Furniture', 2, 250.0, '2023-01-10');
#Dashboard 1
SELECT
 product_category,
 COUNT(*) AS num_orders
FROM
 sales
GROUP BY
 product_category;
#Dashboard 2
SELECT
 order_date,
 SUM(quantity) AS total_quantity,
 SUM(price) AS total_sales_amount
FROM
 sales
WHERE
 order_date BETWEEN '2023-01-01' AND '2023-01-10' -- Specify your desired 
date range here
GROUP BY
 order_date
ORDER BY
 order_date;
#Dashboard 3
SELECT 
 DATE_TRUNC('month', order_date) AS month,
 product_category,
 SUM(quantity * price) AS total_revenue
FROM 
 sales
WHERE 
 order_date BETWEEN '2023-01-01' AND '2023-12-31'
GROUP BY 
 month,
 product_category
ORDER BY 
 month,
 total_revenue DESC;
