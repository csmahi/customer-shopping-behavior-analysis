📊 Customer Shopping Behavior Analysis
End-to-End Data Analytics Case Study | Python · SQL · Power BI
An end-to-end retail analytics project analyzing 3,900 customer transactions across 18 fields to understand purchasing behavior, identify high-value customer segments, evaluate product performance, and generate actionable business recommendations.

Analytics Workflow

Raw Data → Python → SQL → Customer Segmentation → Power BI → Business Recommendations

🎯 Business Problem
A retail business wants to better understand its customers and purchasing behavior.

The analysis focuses on:

Which customer segments generate the most revenue?
Which product categories and products perform best?
Do subscribers behave differently from non-subscribers?
How does purchase frequency relate to revenue?
Which customer groups should marketing prioritize?
How can the business improve customer retention and subscription adoption?
The goal is to move beyond reporting numbers and translate analytical findings into practical business actions.

📌 Project Objectives
Analyze customer purchasing patterns
Identify high-value and loyal customer segments
Evaluate revenue contribution by customer characteristics
Compare subscriber and non-subscriber behavior
Identify top-performing products and categories
Analyze purchase frequency and customer behavior
Build an interactive Power BI dashboard
Translate insights into actionable recommendations
📂 Dataset Overview
The dataset contains 3,900 customer purchase records and 18 fields.

Customer Information
Age
Gender
Location
Subscription Status
Purchase Information
Item Purchased
Category
Purchase Amount
Season
Size
Color
Behavioral & Transaction Metrics
Discount Applied
Promo Code Used
Previous Purchases
Frequency of Purchases
Shipping Type
Review Rating
🔍 Business Questions
The project answers questions such as:

Which customer segments contribute the most revenue?
Which product categories generate the strongest sales?
Which products are most frequently purchased?
Do subscribers demonstrate stronger purchasing behavior?
How does purchase frequency relate to revenue?
Which customer groups should marketing prioritize?
What opportunities exist to improve retention and subscription adoption?
🛠️ Tools & Technologies
Tool	Purpose
Python / Pandas	Data cleaning, preprocessing and EDA
SQL	Business analysis and customer segmentation
CTEs	Multi-step analytical queries
Window Functions	Ranking and category-level analysis
Power BI	Interactive dashboards and KPI reporting
GitHub	Project documentation and version control

🔄 Analytics Workflow
1. Data Preparation — Python
The raw dataset was inspected and prepared for analysis.

Key steps included:

Data quality checks
Missing-value identification
Data consistency checks
Exploratory data analysis
Feature preparation
Review-rating imputation
The dataset contained 37 missing values in Review Rating. These were handled using category-wise median imputation to preserve the distribution of ratings across product categories.

2. Business Analysis — SQL
SQL was used to perform business-focused analysis, including:

Revenue analysis
Customer segmentation
Purchase-frequency analysis
Subscriber vs non-subscriber comparison
Product ranking
Category-level performance
CTE-based analysis
Window functions
Aggregations and conditional logic
3. Customer Segmentation
Customers were grouped according to their previous purchasing behavior:

Segment	Definition
New	1 previous purchase
Returning	2–10 previous purchases
Loyal	More than 10 previous purchases

This segmentation helps distinguish customers based on their level of purchasing engagement.

4. Power BI Dashboard
The Power BI dashboard provides an interactive view of:

Revenue performance
Product performance
Customer segmentation
Subscriber vs non-subscriber behavior
Purchase behavior
Key business insights
## 📊 Dashboard Preview

### 🔹 Sales Overview
![Sales Overview](dashboard_overview.png)

### 🔹 Product Performance
![Product Performance](product_performance.png)

### 🔹 Customer Segmentation
![Customer Segmentation](customer_segmentation.png)

### 🔹 Key Insights
![Key Insights](key_insights.png)

📈 Key Findings
1. Clothing is a major revenue driver
Finding: Clothing is the top-performing category in both sales and revenue.

Business Interpretation: Clothing is an important revenue-generating category and should receive continued attention in merchandising and promotional planning.

Recommendation: Monitor demand closely and use high-performing products within the category for promotions and cross-selling opportunities.

2. Loyal customers are the highest-value segment
Finding: Loyal customers contribute the highest share of total revenue.

Business Interpretation: Customers with stronger purchase histories represent an important source of recurring revenue.

Recommendation: Prioritize retention campaigns, personalized offers, loyalty benefits, and targeted engagement for high-value customers.

3. Frequent buyers generate stronger revenue
Finding: Frequent buyers generate higher revenue than occasional buyers.

Business Interpretation: Purchase frequency is an important indicator of customer value.

Recommendation: Encourage returning customers to purchase more frequently through:

Personalized recommendations
Repeat-purchase reminders
Limited-time offers
Category-based promotions
Loyalty rewards
The goal is to move customers from:

Occasional → Returning → Loyal

4. Subscription represents a retention opportunity
Finding: Subscribers demonstrate stronger purchasing engagement.

Business Interpretation: Subscription status appears to be associated with stronger customer engagement.

Recommendation: Prioritize high-frequency and returning customers for subscription campaigns rather than using a broad, untargeted approach.

5. Younger customers show higher transaction spending
Finding: Younger age groups show higher spending per transaction.

Business Interpretation: Younger customers may represent an attractive target for campaigns focused on higher-value purchases.

Recommendation: Test targeted promotions and personalized recommendations while monitoring whether higher transaction value leads to stronger long-term customer value.

6. Customer satisfaction is generally positive
Finding: The average customer rating is approximately 3.75/5.

Business Interpretation: Overall customer satisfaction is reasonably positive, while lower-rated products may still present improvement opportunities.

Recommendation: Analyze lower-rated products and categories to identify potential issues affecting customer experience and repeat purchases.

💡 Business Recommendations
Based on the analysis, the following actions should be prioritized.

1. Retain High-Value Customers
Loyal customers contribute strongly to revenue.

Recommended actions:

Introduce loyalty-focused campaigns
Offer personalized promotions
Reward repeat purchases
Provide exclusive benefits
Goal: Protect recurring revenue and reduce customer churn.

2. Convert Returning Customers into Loyal Customers
Returning customers already demonstrate purchasing engagement.

Recommended actions:

Provide incentives for the next purchase
Recommend products based on purchase history
Create milestone-based rewards
Use targeted promotional campaigns
Goal: Increase customer lifetime value by encouraging repeat purchases.

3. Increase Subscription Adoption
Recommended actions:

Target frequent and returning customers with relevant subscription offers.

Goal: Convert engaged customers into subscribers and strengthen retention.

4. Protect High-Performing Categories
Clothing is currently the strongest category.

Recommended actions:

Monitor demand
Maintain product availability
Promote high-performing products
Explore cross-selling opportunities
Goal: Protect category revenue while increasing basket value.

5. Use Customer Behavior for Targeted Marketing
Customer Type	Recommended Strategy
New	Welcome campaigns and first-repeat incentives
Returning	Personalized recommendations and targeted offers
Loyal	Retention campaigns, loyalty rewards and exclusive benefits

Goal: Progressively move customers toward higher-value behavior.

🧮 SQL Analysis Examples
Customer Segmentation
WITH customer_type AS (
    SELECT
        customer_id,
        CASE
            WHEN previous_purchases = 1 THEN 'New'
            WHEN previous_purchases BETWEEN 2 AND 10 THEN 'Returning'
            ELSE 'Loyal'
        END AS customer_segment
    FROM customer
)

SELECT
    customer_segment,
    COUNT(*) AS number_of_customers
FROM customer_type
GROUP BY customer_segment;

Top Products by Category
WITH item_counts AS (
    SELECT
        category,
        item_purchased,
        COUNT(*) AS total_orders,
        ROW_NUMBER() OVER (
            PARTITION BY category
            ORDER BY COUNT(*) DESC
        ) AS rank
    FROM customer
    GROUP BY category, item_purchased
)

SELECT
    category,
    item_purchased,
    total_orders
FROM item_counts
WHERE rank <= 3;

Subscriber vs Non-Subscriber Analysis
SELECT
    subscription_status,
    COUNT(customer_id) AS total_customers,
    ROUND(AVG(purchase_amount), 2) AS avg_spend,
    ROUND(SUM(purchase_amount), 2) AS total_revenue
FROM customer
GROUP BY subscription_status
ORDER BY total_revenue DESC;

📊 Project Files
File	Description
customer_shopping_behavior.csv	Raw customer shopping dataset
customer_shopping_behavior_analysis.ipynb	Python analysis, data cleaning, preprocessing and EDA
sql_queries.sql	SQL business analysis and customer segmentation
CustomerBehavior_Analysis_SQL_Python_PBI.pbix	Interactive Power BI dashboard
dashboard_overview.png	Sales and revenue overview
product_performance.png	Product and category performance
customer_segmentation.png	Customer segmentation analysis
key_insights.png	Summary of key business insights

🚀 How to Explore the Project
Step 1 — Dataset
Start with:

customer_shopping_behavior.csv

Step 2 — Python Analysis
Open:

customer_shopping_behavior_analysis.ipynb

Review the data cleaning, preprocessing and exploratory analysis.

Step 3 — SQL Analysis
Open:

sql_queries.sql

Review the CTEs, window functions, aggregations and customer segmentation logic.

Step 4 — Power BI Dashboard
Open:

CustomerBehavior_Analysis_SQL_Python_PBI.pbix

Explore the customer, product, revenue and segmentation insights interactively.

🎯 Business Value
This project demonstrates how raw transactional data can be transformed into business decisions.

Data → Information → Insight → Recommendation
The analysis focuses on:

Customer retention
Customer segmentation
Subscription conversion
Purchase-frequency growth
Product/category optimization
Customer experience
The key objective is not simply to report what happened, but to identify what the business should do next.

🧠 Skills Demonstrated
Data Cleaning
Exploratory Data Analysis
Python / Pandas
SQL
Common Table Expressions (CTEs)
Window Functions
Aggregations
Customer Segmentation
Revenue Analysis
Power BI
KPI Development
Business Intelligence
Business Storytelling
Data-Driven Recommendations
👤 Author
Chandrashekar Sharma M
Data Analytics | Python | SQL | Power BI

GitHub: https://github.com/csmahi
LinkedIn: https://www.linkedin.com/in/chandrashekar-m-807267296/
⭐ Project Summary
Customer Shopping Behavior Analysis is an end-to-end analytics project demonstrating how Python, SQL and Power BI can be used to transform customer transaction data into actionable business insights.

The project combines technical analysis with business thinking, focusing on customer behavior, revenue drivers, segmentation, retention and data-driven recommendations.
