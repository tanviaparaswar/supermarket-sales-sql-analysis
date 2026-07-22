# Supermarket Sales SQL Analysis

## **SECTION 1: TABLE SETUP**

```sql
CREATE TABLE IF NOT EXISTS sales (
   invoice_id VARCHAR(30) NOT NULL PRIMARY KEY,
   branch VARCHAR(3) NOT NULL,
   city VARCHAR(30) NOT NULL,
   customer_type VARCHAR(30) NOT NULL,
   gender VARCHAR(10) NOT NULL,
   product_line VARCHAR(100) NOT NULL,
   unit_price DECIMAL(10,2) NOT NULL,
   quantity INT NOT NULL,
   VAT FLOAT(6,4) NOT NULL,
   total DECIMAL(10,2) NOT NULL,
   date DATE NOT NULL,
   time TIMESTAMP NOT NULL,
   payment_method DECIMAL(10,2) NOT NULL,
   cogs DECIMAL(10,2) NOT NULL,
   gross_margin_percentage FLOAT(11,9) NOT NULL,
   gross_income DECIMAL(10,2),
   rating FLOAT(2,1)
);

INSERT INTO sales VALUES
('INV001','A','Pune','Member','Male','Electronics',55000.00,2,550.5000,111100.00,'2024-01-05','2024-01-05 10:15:00',2.00,110000.00,4.761904761,5500.00,4.5),
('INV002','B','Mumbai','Normal','Female','Fashion',2500.00,5,125.2500,12625.00,'2024-01-06','2024-01-06 12:20:00',1.00,12500.00,4.761904761,625.00,4.2),
('INV003','C','Delhi','Member','Male','Sports',3200.00,3,96.0000,9696.00,'2024-01-07','2024-01-07 15:45:00',3.00,9600.00,4.761904761,480.00,4.6),
('INV004','A','Pune','Normal','Female','Accessories',900.00,10,45.0000,4545.00,'2024-01-08','2024-01-08 11:30:00',2.00,4500.00,4.761904761,225.00,4.0),
('INV005','B','Mumbai','Member','Male','Furniture',8500.00,1,85.0000,8585.00,'2024-01-09','2024-01-09 16:10:00',1.00,8500.00,4.761904761,425.00,4.4),
('INV006','C','Delhi','Normal','Female','Electronics',22000.00,2,220.0000,44440.00,'2024-01-10','2024-01-10 09:40:00',2.00,44000.00,4.761904761,2200.00,4.3),
('INV007','A','Pune','Member','Male','Fashion',1800.00,6,54.0000,10854.00,'2024-01-11','2024-01-11 13:25:00',1.00,10800.00,4.761904761,540.00,4.1),
('INV008','B','Mumbai','Normal','Female','Sports',6000.00,2,120.0000,12120.00,'2024-01-12','2024-01-12 17:35:00',3.00,12000.00,4.761904761,600.00,4.7),
('INV009','C','Delhi','Member','Male','Accessories',3000.00,4,60.0000,12120.00,'2024-01-13','2024-01-13 10:05:00',2.00,12000.00,4.761904761,600.00,4.2),
('INV010','A','Pune','Normal','Female','Furniture',5000.00,2,100.0000,10100.00,'2024-01-14','2024-01-14 14:50:00',1.00,10000.00,4.761904761,500.00,4.3),
('INV011','B','Mumbai','Member','Male','Electronics',48000.00,1,480.0000,48480.00,'2024-01-15','2024-01-15 18:20:00',2.00,48000.00,4.761904761,2400.00,4.8),
('INV012','C','Delhi','Normal','Female','Fashion',4500.00,3,135.0000,13635.00,'2024-01-16','2024-01-16 11:15:00',1.00,13500.00,4.761904761,675.00,4.1),
('INV013','A','Pune','Member','Male','Sports',14000.00,2,280.0000,28280.00,'2024-01-17','2024-01-17 15:00:00',3.00,28000.00,4.761904761,1400.00,4.5),
('INV014','B','Mumbai','Normal','Female','Accessories',5200.00,2,104.0000,10504.00,'2024-01-18','2024-01-18 09:25:00',2.00,10400.00,4.761904761,520.00,4.2),
('INV015','C','Delhi','Member','Male','Furniture',9500.00,1,95.0000,9595.00,'2024-01-19','2024-01-19 12:45:00',1.00,9500.00,4.761904761,475.00,4.0),
('INV016','A','Pune','Normal','Female','Electronics',32000.00,1,320.0000,32320.00,'2024-01-20','2024-01-20 16:30:00',2.00,32000.00,4.761904761,1600.00,4.6),
('INV017','B','Mumbai','Member','Male','Fashion',2500.00,4,100.0000,10100.00,'2024-01-21','2024-01-21 10:55:00',1.00,10000.00,4.761904761,500.00,4.4),
('INV018','C','Delhi','Normal','Female','Sports',6000.00,3,180.0000,18180.00,'2024-01-22','2024-01-22 13:10:00',3.00,18000.00,4.761904761,900.00,4.7),
('INV019','A','Pune','Member','Male','Accessories',1800.00,5,90.0000,9090.00,'2024-01-23','2024-01-23 17:40:00',2.00,9000.00,4.761904761,450.00,4.1),
('INV020','B','Mumbai','Normal','Female','Furniture',8500.00,2,170.0000,17170.00,'2024-01-24','2024-01-24 11:05:00',1.00,17000.00,4.761904761,850.00,4.3);
```

## **SECTION 2: DATABASE MODIFICATION**

```sql
-- 1. Add a new column time_of_day
ALTER TABLE sales ADD COLUMN time_of_day VARCHAR(20);

UPDATE sales
SET time_of_day = (
 CASE
   WHEN HOUR(time) BETWEEN 5 AND 11 THEN 'Morning'
   WHEN HOUR(time) BETWEEN 12 AND 16 THEN 'Afternoon'
   WHEN HOUR(time) BETWEEN 17 AND 20 THEN 'Evening'
   ELSE 'Night'
 END
);

-- 2. Add a new column day_name
ALTER TABLE sales ADD COLUMN day_name VARCHAR(15);

UPDATE sales
SET day_name = DAYNAME(date);

-- 3. Add a new column month_name
ALTER TABLE sales ADD COLUMN month_name VARCHAR(15);

UPDATE sales
SET month_name = MONTHNAME(date);
```

## **SECTION 3: GENERIC QUESTIONS**

```sql
-- 1. How many unique cities does the data have?
SELECT COUNT(DISTINCT city) AS unique_cities
FROM sales;

-- 2. In which city is each branch located?
SELECT DISTINCT branch, city
FROM sales
ORDER BY branch;
```

## **SECTION 4: PRODUCT ANALYSIS QUESTIONS**

```sql
-- 1. How many unique product lines does the data have?
SELECT COUNT(DISTINCT product_line) AS unique_product_lines
FROM sales;

-- 2. What is the most common payment method?
SELECT payment_method, COUNT(*) AS uses
FROM sales
GROUP BY payment_method
ORDER BY uses DESC
LIMIT 1;

-- 3. What is the most selling product line?
SELECT product_line, SUM(quantity) AS total_units_sold
FROM sales
GROUP BY product_line
ORDER BY total_units_sold DESC
LIMIT 1;

-- 4. What is the total revenue by month?
SELECT month_name, SUM(total) AS total_revenue
FROM sales
GROUP BY month_name
ORDER BY total_revenue DESC;

-- 5. Which month had the largest COGS?
SELECT month_name, SUM(cogs) AS total_cogs
FROM sales
GROUP BY month_name
ORDER BY total_cogs DESC
LIMIT 1;

-- 6. Which product line had the largest revenue?
SELECT product_line, SUM(total) AS total_revenue
FROM sales
GROUP BY product_line
ORDER BY total_revenue DESC
LIMIT 1;

-- 7. Which city generated the largest revenue?
SELECT city, SUM(total) AS total_revenue
FROM sales
GROUP BY city
ORDER BY total_revenue DESC
LIMIT 1;

-- 8. Which product line had the largest VAT amount?
SELECT product_line, SUM(VAT) AS total_vat
FROM sales
GROUP BY product_line
ORDER BY total_vat DESC
LIMIT 1;

-- 9. Fetch each product line and classify it as "Good" or "Bad" based on average sales
SELECT
 product_line,
 AVG(total) AS avg_sales,
 CASE
   WHEN AVG(total) >= (SELECT AVG(total) FROM sales) THEN 'Good'
   ELSE 'Bad'
 END AS sales_rating
FROM sales
GROUP BY product_line
ORDER BY avg_sales DESC;

-- 10. Which branch sold more products than the average quantity sold?
SELECT branch, SUM(quantity) AS total_quantity
FROM sales
GROUP BY branch
HAVING SUM(quantity) > (
 SELECT AVG(branch_qty) FROM (
   SELECT branch, SUM(quantity) AS branch_qty
   FROM sales
   GROUP BY branch
 ) AS branch_totals
)
ORDER BY total_quantity DESC;

-- 11. What is the most common product line by gender?
SELECT gender, product_line, COUNT(*) AS purchase_count
FROM sales
GROUP BY gender, product_line
ORDER BY gender, purchase_count DESC;

-- 12. What is the average rating of each product line?
SELECT product_line, ROUND(AVG(rating), 2) AS avg_rating
FROM sales
GROUP BY product_line
ORDER BY avg_rating DESC;
```

## **SECTION 5: SALES ANALYSIS QUESTIONS**

```sql
-- 1. Number of sales made in each time of the day per weekday
SELECT day_name, time_of_day, COUNT(*) AS number_of_sales
FROM sales
GROUP BY day_name, time_of_day
ORDER BY day_name,
 FIELD(time_of_day, 'Morning', 'Afternoon', 'Evening', 'Night');

-- 2. Which customer type brings the most revenue?
SELECT customer_type, SUM(total) AS total_revenue
FROM sales
GROUP BY customer_type
ORDER BY total_revenue DESC
LIMIT 1;

-- 3. Which city has the largest VAT percentage?
SELECT city, ROUND(AVG(VAT / total) * 100, 2) AS avg_vat_percentage
FROM sales
GROUP BY city
ORDER BY avg_vat_percentage DESC
LIMIT 1;

-- 4. Which customer type pays the highest VAT amount?
SELECT customer_type, SUM(VAT) AS total_vat
FROM sales
GROUP BY customer_type
ORDER BY total_vat DESC
LIMIT 1;
```

## **SECTION 6: CUSTOMER ANALYSIS QUESTIONS**

```sql
-- 1. How many unique customer types does the data have?
SELECT COUNT(DISTINCT customer_type) AS unique_customer_types
FROM sales;

-- 2. How many unique payment methods does the data have?
SELECT COUNT(DISTINCT payment_method) AS unique_payment_methods
FROM sales;

-- 3. What is the most common customer type?
SELECT customer_type, COUNT(*) AS count
FROM sales
GROUP BY customer_type
ORDER BY count DESC
LIMIT 1;

-- 4. What is the gender of most customers?
SELECT gender, COUNT(*) AS count
FROM sales
GROUP BY gender
ORDER BY count DESC
LIMIT 1;

-- 5. Which customer type buys the most?
SELECT customer_type, SUM(quantity) AS total_quantity
FROM sales
GROUP BY customer_type
ORDER BY total_quantity DESC
LIMIT 1;

-- 6. What is the gender distribution per branch?
SELECT branch, gender, COUNT(*) AS count
FROM sales
GROUP BY branch, gender
ORDER BY branch, gender;

-- 7. During which time of the day do customers give the most ratings?
SELECT time_of_day, COUNT(rating) AS ratings_given
FROM sales
GROUP BY time_of_day
ORDER BY ratings_given DESC
LIMIT 1;

-- 8. Which time of the day receives the highest ratings per branch?
SELECT branch, time_of_day, ROUND(AVG(rating), 2) AS avg_rating
FROM sales
GROUP BY branch, time_of_day
ORDER BY branch, avg_rating DESC;

-- 9. Which day of the week has the best average rating?
SELECT day_name, ROUND(AVG(rating), 2) AS avg_rating
FROM sales
GROUP BY day_name
ORDER BY avg_rating DESC
LIMIT 1;

-- 10. Which day of the week has the best average rating per branch?
SELECT branch, day_name, ROUND(AVG(rating), 2) AS avg_rating
FROM sales
GROUP BY branch, day_name
ORDER BY branch, avg_rating DESC;
```
