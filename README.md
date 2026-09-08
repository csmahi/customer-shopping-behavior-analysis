# 📊 Customer Shopping Behavior Analysis  

End-to-End Data Analytics Project using Python, SQL, and Power BI

---

## 📌 Project Overview  

This project analyzes customer shopping behavior using transactional data from **3,900 purchases** across multiple product categories.

The objective is to generate actionable insights into:
- Customer spending patterns  
- Product preferences  
- Customer segmentation  
- Purchase frequency and retention behavior  

These insights support data-driven decision-making in marketing, sales, and customer experience strategies.

---

## 📂 Dataset Summary  

- Total Records: 3,900  
- Total Features: 18  

### Key Data Categories:
- Customer Demographics: Age, Gender, Location, Subscription Status  
- Purchase Information: Item Purchased, Category, Purchase Amount, Season, Size, Color  
- Behavioral Metrics: Discount Applied, Promo Code Used, Previous Purchases, Frequency of Purchases, Shipping Type, Review Rating  

---

## 🧹 Data Preprocessing (Python)

- Checked missing and inconsistent values  
- Identified 37 missing values in Review Rating  
- Applied category-wise median imputation  
- Cleaned dataset for analysis  

---

## 🛠 Tools & Technologies

- Python (Pandas)  
- SQL (Data analysis & querying)  
- Power BI (Dashboard visualization)  

---

## 🧠 Skills Demonstrated

- Data Cleaning & Preprocessing  
- Exploratory Data Analysis (EDA)  
- SQL (CTEs, Window Functions, Aggregations)  
- Data Visualization (Power BI)  
- Business Insight Generation

---

## 📁 Project Files

- customer_shopping_behavior.csv → Dataset  
- customer_shopping_behavior_analysis.ipynb → Python notebook  
- sql_queries.sql → SQL queries  
- CustomerBehavior_Analysis_SQL_Python_PBI.pbix → Power BI file  
- dashboard_overview.png → Sales overview dashboard  
- product_performance.png → Product insights  
- customer_segmentation.png → Segmentation analysis  
- key_insights.png → Summary insights
  
---

## 🔄 Project Workflow

1. Data cleaning using Python  
2. Data analysis using SQL  
3. Dashboard creation using Power BI  

---

## 🧾 Sample SQL Queries  

### 1. Customer Segmentation (CTE)

```sql
WITH customer_type AS (
    SELECT customer_id,
           CASE 
               WHEN previous_purchases = 1 THEN 'New'
               WHEN previous_purchases BETWEEN 2 AND 10 THEN 'Returning'
               ELSE 'Loyal'
           END AS customer_segment
    FROM customer
)
SELECT customer_segment,
       COUNT(*) AS number_of_customers
FROM customer_type
GROUP BY customer_segment;
```

### 2. Top Products per Category
```sql
WITH item_counts AS (
    SELECT category,
           item_purchased,
           COUNT(*) AS total_orders,
           ROW_NUMBER() OVER (
               PARTITION BY category
               ORDER BY COUNT(*) DESC
           ) AS rank
    FROM customer
    GROUP BY category, item_purchased
)
SELECT category, item_purchased, total_orders
FROM item_counts
WHERE rank <= 3;
```

### 3. Subscriber vs Non-Subscriber Spending

```sql
SELECT subscription_status,
       COUNT(customer_id) AS total_customers,
       ROUND(AVG(purchase_amount), 2) AS avg_spend,
       ROUND(SUM(purchase_amount), 2) AS total_revenue
FROM customer
GROUP BY subscription_status
ORDER BY total_revenue DESC;
```

📁 Full SQL File  

👉 [View SQL Queries](sql_queries.sql)

## 📊 Dashboard Preview

### 🔹 Sales Overview
![Sales Overview](dashboard_overview.png)

### 🔹 Product Performance
![Product Performance](product_performance.png)

### 🔹 Customer Segmentation
![Customer Segmentation](customer_segmentation.png)

### 🔹 Key Insights
![Key Insights](key_insights.png)


## 🔍 Key Insights

- Clothing is the top-performing category in both sales and revenue  
- Loyal customers contribute the highest share of total revenue  
- Frequent buyers generate significantly higher revenue than occasional buyers  
- Younger age groups spend more per transaction  
- Average customer rating is ~3.75, indicating overall positive satisfaction  
- Subscription users demonstrate stronger retention behavior


## 📈 Business Impact

- Identified high-value customer segments driving the majority of revenue  
- Enabled targeted marketing strategies based on customer behavior  
- Improved understanding of purchase frequency and retention patterns  
- Highlighted top-performing product categories for revenue optimization
  


## 🚀 How to Run This Project

1. Clone the repository  
2. Run the Python notebook for data preprocessing  
3. Execute SQL queries from `sql_queries.sql`  
4. Open the Power BI file to explore the dashboard  

 


   


---

## 👤 Author

**Chandrashekar Sharma M**

- GitHub: https://github.com/csmahi  
- LinkedIn: https://www.linkedin.com/in/chandrashekar-m-807267296/  
