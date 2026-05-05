# 📊 Customer Shopping Behavior Analysis  
### End-to-End Data Analytics Project (Python + SQL + Power BI)

---

## 📌 Project Overview

This project analyzes customer shopping behavior using transactional data from 3,900 purchases across multiple product categories.

The objective is to generate actionable insights into:

- Customer spending patterns  
- Product preferences  
- Customer segmentation  
- Purchase frequency and retention behavior  

These insights support data-driven decision-making in marketing, sales, and customer experience strategies.

---

## 📂 Dataset Summary

- **Total Records:** 3,900  
- **Total Features:** 18  

### Key Data Categories:

- **Customer Demographics:** Age, Gender, Location, Subscription Status  
- **Purchase Information:** Item Purchased, Category, Purchase Amount, Season, Size, Color  
- **Behavioral Metrics:** Discount Applied, Promo Code Used, Previous Purchases, Frequency of Purchases, Shipping Type, Review Rating  

---

## 🧹 Data Preprocessing (Python)

- Checked for missing and inconsistent values  
- Identified **37 missing values** in the *Review Rating* column  
- Applied category-wise median imputation  
- Ensured clean and analysis-ready dataset  

---

## 🛠 Tools & Technologies

- **Python:** Pandas, NumPy (data cleaning and preprocessing)  
- **SQL:** Data extraction, transformation, and analysis  
- **Power BI:** Dashboard creation and visualization  

---

## 📁 Project Files

- 📊 `customer_data.csv` → Dataset used for analysis  
- 📓 `customer_analysis.ipynb` → Python notebook for data cleaning and EDA  
- 🧾 `sql_queries.sql` → Main SQL script with all queries  
- 📈 `dashboard_image.png` → Power BI dashboard screenshot  

---

## 🔄 Project Workflow

1. Data cleaning and preprocessing using Python  
2. Data analysis using SQL queries  
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
2. Top Products per Category
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
3. Subscriber vs Non-Subscriber Spending
SELECT subscription_status,
       COUNT(customer_id) AS total_customers,
       ROUND(AVG(purchase_amount), 2) AS avg_spend,
       ROUND(SUM(purchase_amount), 2) AS total_revenue
FROM customer
GROUP BY subscription_status
ORDER BY total_revenue DESC;
📁 Full SQL File

👉 All queries are available here:
[📄 sql_queries.sql](./sql_queries.sql)

📊 Power BI Dashboard
![Customer Behavior Analysis Dashboard](Screenshots/dashboard.png)

Below is the dashboard visualizing key business insights:

🔍 Key Insights
Clothing is the top-performing category in sales and revenue
Loyal customers contribute the highest revenue
Frequent buyers generate significantly higher revenue
Younger age groups spend more per transaction
Average rating is 3.75, indicating positive customer satisfaction
Subscription users show stronger retention behavior
🚀 How to Run This Project
Clone the repository
Run Python notebook for preprocessing
Execute SQL queries from sql_queries.sql
Open Power BI dashboard image or .pbix file
👤 Author

Your Name
🔗 LinkedIn: [Add your link here]
💻 GitHub: [Add your link here]
