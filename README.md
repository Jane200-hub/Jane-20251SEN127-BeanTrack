# PLSQL Assignment One – Sunrise Supermarket

## Student Information

- **Student Name:** Kacyeye Igihozo Jane
- **Student ID:** 20251SEN127
- **DBMS Used:** PostgreSQL
- **Repository Name:** `assignment_1_KacyeyeIgihozoJane-20251SEN127`

---

## 1. Business Scenario

Sunrise Supermarket sells different products to customers. Customers place orders, and each order can contain one or more products.

The management of Sunrise Supermarket wants to understand customer purchasing behavior, product sales, and sales trends. This database assignment uses SQL queries to retrieve and analyze the required information.

The database contains the following main tables:

- `customers` – stores customer information.
- `products` – stores product names, categories, and prices.
- `orders` – stores customer orders and order dates.
- `order_items` – stores the products and quantities included in each order.

---

## 2. Database Data

The database contains:

- **6 customers**
- **8 products**
- **5 product categories**
- **15 orders**
- **30 order items**
- Orders occurring across multiple dates in September 2026.

The product categories include Dairy, Bakery, Grains, Groceries, and Beverages.

---

## 3. How to Run the Assignment

### Step 1: Install PostgreSQL

PostgreSQL was used as the database management system for this assignment.

### Step 2: Create the Database

The database used is:

```text
sunrise_supermarket
```

### Step 3: Connect to PostgreSQL

Open PostgreSQL/PSQL and connect to the `sunrise_supermarket` database.

Example:

```text
psql -U postgres -d sunrise_supermarket
```

### Step 4: Run the SQL Code

The SQL file included in this repository contains the table creation, data insertion, and required queries.

The main SQL file is:

```text
assignment_1.sql
```

---

# 4. Required SQL Queries

## JOIN Queries

### Query 1: Every Order with Customer Name, City and Order Date

This query uses an INNER JOIN between the `orders` and `customers` tables. It displays the order ID, customer name, city, and order date.

```sql
SELECT o.order_id, c.customer_name, c.city, o.order_date FROM orders o INNER JOIN customers c ON o.customer_id = c.customer_id ORDER BY o.order_date;
```

### Screenshot 1 – Query 1 Result

**INSERT SCREENSHOT HERE**

Suggested screenshot filename:

`query1_order_customer.png`

---

### Query 2: Order Items with Product Information

This query joins `order_items` with `products` to show the product name, category, price, and quantity for every order item.

```sql
SELECT oi.order_item_id, oi.order_id, p.product_name, p.category, p.price, oi.quantity FROM order_items oi INNER JOIN products p ON oi.product_id = p.product_id ORDER BY oi.order_id;
```

### Screenshot 2 – Query 2 Result

**INSERT SCREENSHOT HERE**

Suggested screenshot filename:

`query2_order_items.png`

---

### Query 3: All Customers and Their Orders

This query uses a LEFT JOIN so that all customers are included, even if a customer does not have an order. Customers with no matching order would have NULL values in the order columns.

```sql
SELECT c.customer_id, c.customer_name, c.city, o.order_id, o.order_date FROM customers c LEFT JOIN orders o ON c.customer_id = o.customer_id ORDER BY c.customer_id, o.order_date;
```

### Screenshot 3 – Query 3 Result

**INSERT SCREENSHOT HERE**

Suggested screenshot filename:

`query3_customers_orders.png`

---

# 5. CTE Query

## Query 4: Customers Spending Above the Average

A Common Table Expression (CTE) is used to first calculate the total spending for each customer. The main query then selects customers whose total spending is higher than the average customer spending.

The total spending is calculated using:

`quantity × price`

```sql
WITH customer_totals AS (SELECT c.customer_id, c.customer_name, COALESCE(SUM(oi.quantity * p.price), 0) AS total_spend FROM customers c LEFT JOIN orders o ON c.customer_id = o.customer_id LEFT JOIN order_items oi ON o.order_id = oi.order_id LEFT JOIN products p ON oi.product_id = p.product_id GROUP BY c.customer_id, c.customer_name) SELECT customer_id, customer_name, total_spend FROM customer_totals WHERE total_spend > (SELECT AVG(total_spend) FROM customer_totals) ORDER BY total_spend DESC;
```

### Screenshot 4 – Query 4 Result

**INSERT SCREENSHOT HERE**

Suggested screenshot filename:

`query4_cte_above_average.png`

---

# 6. Window Function Queries

## Query 5: Rank Customers by Total Amount Spent

This query calculates each customer's total spending and uses the `RANK()` window function to rank customers from the highest spending amount to the lowest.

```sql
WITH customer_totals AS (SELECT c.customer_id, c.customer_name, COALESCE(SUM(oi.quantity * p.price), 0) AS total_spend FROM customers c LEFT JOIN orders o ON c.customer_id = o.customer_id LEFT JOIN order_items oi ON o.order_id = oi.order_id LEFT JOIN products p ON oi.product_id = p.product_id GROUP BY c.customer_id, c.customer_name) SELECT customer_id, customer_name, total_spend, RANK() OVER (ORDER BY total_spend DESC) AS spending_rank FROM customer_totals ORDER BY spending_rank;
```

### Screenshot 5 – Query 5 Result

**INSERT SCREENSHOT HERE**

Suggested screenshot filename:

`query5_customer_ranking.png`

---

## Query 6: Number Each Customer's Orders

This query uses `ROW_NUMBER()` to number each customer's orders according to the date they were placed.

```sql
SELECT order_id, customer_id, order_date, ROW_NUMBER() OVER (PARTITION BY customer_id ORDER BY order_date) AS customer_order_number FROM orders ORDER BY customer_id, order_date;
```

### Screenshot 6 – Query 6 Result

**INSERT SCREENSHOT HERE**

Suggested screenshot filename:

`query6_order_numbering.png`

---

## Query 7: Running Total Revenue Over Time

This query first calculates daily revenue and then uses a window function to calculate the running total revenue in chronological order.

Revenue is calculated as:

`quantity × price`

```sql
WITH daily_revenue AS (SELECT o.order_date, SUM(oi.quantity * p.price) AS daily_revenue FROM orders o JOIN order_items oi ON o.order_id = oi.order_id JOIN products p ON oi.product_id = p.product_id GROUP BY o.order_date) SELECT order_date, daily_revenue, SUM(daily_revenue) OVER (ORDER BY order_date) AS running_total_revenue FROM daily_revenue ORDER BY order_date;
```

### Screenshot 7 – Query 7 Result

**INSERT SCREENSHOT HERE**

Suggested screenshot filename:

`query7_running_revenue.png`

---

## Query 8: Days Between Customer Orders

This query uses the `LAG()` window function to find the previous order date for each customer. It then calculates the number of days between the current order and the previous order.

Customers with more than one order are included.

```sql
WITH customer_orders AS (SELECT order_id, customer_id, order_date, LAG(order_date) OVER (PARTITION BY customer_id ORDER BY order_date) AS previous_order_date, COUNT(*) OVER (PARTITION BY customer_id) AS order_count FROM orders) SELECT order_id, customer_id, order_date, previous_order_date, order_date - previous_order_date AS days_between_orders FROM customer_orders WHERE order_count > 1 AND previous_order_date IS NOT NULL ORDER BY customer_id, order_date;
```

### Screenshot 8 – Query 8 Result

**INSERT SCREENSHOT HERE**

Suggested screenshot filename:

`query8_days_between_orders.png`

---

# 7. Business Interpretation

The SQL queries provide useful information that can help Sunrise Supermarket management understand its customers and sales.

### Customer Information

The JOIN queries connect customer information with their orders. This allows management to see which customers placed orders, when the orders were placed, and where the customers are located.

### Product and Order Information

The order-item query shows which products were included in orders, their categories, prices, and quantities. This can help management understand which products are being purchased.

### Customer Spending

The CTE query identifies customers whose spending is above the average. This can help management identify customers who contribute a larger amount of sales.

### Customer Ranking

The ranking query orders customers according to their total spending. This provides a clear view of customer spending levels.

### Order Frequency

The order-numbering and days-between-orders queries help management understand how frequently customers place orders.

### Revenue Trend

The running-total query shows how revenue accumulates over time. This can help management monitor sales growth across the order dates.

---

# 8. Challenges and Resolutions

### Challenge 1: Creating the Database Tables

The database required several related tables, including customers, products, orders, and order items.

**Resolution:** The tables were created using primary keys and foreign keys to establish relationships between the tables.

### Challenge 2: Joining Related Tables

Some queries required information from multiple tables.

**Resolution:** INNER JOIN and LEFT JOIN were used with the appropriate foreign-key relationships.

### Challenge 3: Calculating Customer Spending

Customer spending required combining product prices with quantities across multiple order items.

**Resolution:** The calculation `quantity * price` was used with `SUM()` and grouped by customer.

### Challenge 4: Using CTEs and Window Functions

CTEs and window functions required understanding how intermediate results and calculations work.

**Resolution:** CTEs were used to create temporary result sets, while `RANK()`, `ROW_NUMBER()`, `LAG()`, and windowed `SUM()` were used for the required analysis.

---

# 9. Screenshots Checklist

Before submitting, make sure the following screenshots have been added to this README:

- [ ] Screenshot 1 – Query 1 JOIN result
- [ ] Screenshot 2 – Query 2 JOIN result
- [ ] Screenshot 3 – Query 3 LEFT JOIN result
- [ ] Screenshot 4 – Query 4 CTE result
- [ ] Screenshot 5 – Query 5 customer ranking result
- [ ] Screenshot 6 – Query 6 order numbering result
- [ ] Screenshot 7 – Query 7 running revenue result
- [ ] Screenshot 8 – Query 8 days-between-orders result

Replace each **INSERT SCREENSHOT HERE** section with the corresponding screenshot after uploading the image to the GitHub repository.

---

# 10. Repository Submission

The GitHub repository should be named:

```text
assignment_1_KacyeyeIgihozoJane-20251SEN127
```

The repository should contain at least:

```text
assignment_1_KacyeyeJane-20251SEN127/
│
├── README.md
└── assignment_1.sql
```

After pushing the files to GitHub, copy the repository URL and submit the URL as required by the instructor.

---

## 11. Conclusion

This assignment demonstrates the use of PostgreSQL SQL to manage and analyze supermarket data. INNER JOIN, LEFT JOIN, CTEs, and window functions were used to retrieve customer information, analyze product orders, calculate customer spending, rank customers, number orders, calculate running revenue, and determine the number of days between customer orders.
