# Zepto-Sales-Analytics

PowerBI Analysis
•	Built an interactive Power BI dashboard for Zepto sales and campaign analysis

•	 Tracked key metrics: orders, revenue, discounts, influencer activity


•	 Visuals included:
 – Revenue by city
 – Top-selling products
 – Category-wise orders
 – Influencer impact on sales

•	Used DAX to calculate and analyze discount effectiveness


•	Added dynamic slicers for city, category, and influencer filters
 Delivered actionable insights for pricing, product focus, and campaign strategy

SQL - Solve business Problem

-- Basic (Level 1)
-- Q1. Top 3 cities by total revenue

select city, sum(total_revenue) as total_revenue
from zepto
group by 1
order by 2 desc
limit 3;

-- Q2. Product with the highest number of orders.

select product_name, count(*) as order_count
from zepto
group by 1
order by 2 desc;

-- Category-wise average discount_price

select category, round (avg(discount_price) ,1) as avg_discount_price
from zepto
group by 1
order by 2 desc;

-- Number of products where current price < original price

select count(*)
from zepto
where current_price < original_price;

select * from zepto;

-- Count of influencer campaigns by category

select category, influencer_active, count(*) as counts
from zepto
group by 1,2
order by 1;

-- Intermediate (Level 2)
-- Q1. Revenue difference due to discounts (Original vs Current Price * Orders)

SELECT 
    Category,
    Original_Price,
    Current_Price,
    Orders,
    (Original_Price * Orders) AS Original_Revenue,
    (Current_Price * Orders) AS Current_Revenue,
    (Original_Price * Orders - Current_Price * Orders) AS Revenue_Difference
FROM 
    zepto;


-- Q2. Products with high discounts_price but low orders

select product_name, discount_price, count(*) as orders
from zepto
group by 1,2 
order by 2 desc, 3;

-- Q3. Avg revenue per order by city

select city, round (sum(total_revenue) / sum(orders) ,2) as revenue_per_order
from zepto
group by 1;


-- Q4. Top products influenced by influencer campaigns

select product_name, count(Influencer_Active) as influencer_campaigns
from zepto
where Influencer_Active = "Yes"
group by 1
order by 2 desc;

-- Q5. Compare influencer vs non-influencer campaign revenue

```
select Influencer_Active, sum(total_revenue) as revenue
from zepto
group by 1
```
