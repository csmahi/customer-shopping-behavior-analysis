📊 Customer Shopping Behavior Analysis
End-to-End Data Analytics Case Study | Python · SQL · Power BI
An end-to-end retail analytics project analyzing 3,900 customer transactions across 18 fields to understand purchasing behavior, identify high-value customer segments, evaluate product performance, and generate actionable business recommendations.

The project follows a complete analytics workflow:

Raw Data → Python Data Cleaning & EDA → SQL Business Analysis → Customer Segmentation → Power BI Dashboard → Business Recommendations

🎯 Business Problem
A retail business wants to better understand its customers and purchasing behavior.

The key business challenge is to identify:

Which customer segments generate the most revenue?
Which product categories and products perform best?
Do subscribers behave differently from non-subscribers?
How does purchase frequency relate to revenue?
Which customer groups should marketing prioritize?
Where are there opportunities to improve customer retention and subscription adoption?
The goal is not only to analyze the data, but to translate the analysis into business actions.

📌 Project Objectives
This project aims to:

Analyze customer purchasing patterns
Identify high-value and loyal customer segments
Evaluate revenue contribution by customer characteristics
Compare subscriber and non-subscriber behavior
Identify top-performing product categories and products
Analyze purchase frequency and customer retention patterns
Build an interactive Power BI dashboard for decision-making
Translate analytical findings into actionable recommendations
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
The analysis answers the following questions:

Which customer segments contribute the most revenue?
Which product categories generate the strongest sales performance?
Which products are most frequently purchased within each category?
Do subscribed customers demonstrate stronger purchasing behavior?
How does purchase frequency relate to revenue?
Which age groups contribute more to spending?
What does customer segmentation reveal about loyalty and retention?
Which customer groups should marketing prioritize?
What actions could improve customer retention and subscription adoption?
🛠️ Tools & Technologies
Tool	Purpose
Python	Data cleaning, preprocessing and EDA
Pandas	Data manipulation and transformation
SQL	Business analysis and customer segmentation
CTEs	Multi-step analytical queries
Window Functions	Ranking and category-level analysis
Power BI	Interactive dashboard and KPI reporting
GitHub	Project version control and documentation

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
SQL was used to answer business-focused questions rather than simply retrieve data.

The analysis includes:

Revenue aggregations
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

This segmentation helps the business distinguish between customers who are new, returning, and highly engaged.

4. Power BI Dashboard
The Power BI dashboard converts the analysis into an interactive reporting layer.

The dashboard covers:

Revenue performance
Product performance
Customer segmentation
Subscriber vs non-subscriber analysis
Purchase behavior
Key customer insights
Dashboard Preview
Sales Overview
Product Performance
Customer Segmentation
Key Insights
📈 Key Findings
The analysis produced several important business insights.

1. Clothing is a major revenue driver
Finding: Clothing is the top-performing category in both sales and revenue.

Business interpretation: Clothing represents an important revenue-generating category and should receive continued attention in merchandising, promotions, and inventory planning.

Recommendation: Monitor clothing demand closely and use high-performing products within this category as anchors for promotional campaigns and cross-selling strategies.

2. Loyal customers are the highest-value segment
Finding: Loyal customers contribute the highest share of total revenue.

Business interpretation: Customers with stronger purchase histories represent an important source of recurring revenue.

Recommendation: Prioritize retention strategies for loyal customers through personalized offers, early access to promotions, loyalty benefits, and targeted engagement campaigns.

The objective should be to protect the existing high-value customer base, not simply acquire more customers.

3. Frequent buyers generate stronger revenue
Finding: Frequent buyers generate significantly higher revenue than occasional buyers.

Business interpretation: Purchase frequency is an important indicator of customer value.

Recommendation: Develop campaigns designed to increase purchase frequency among returning customers.

Examples include:

Personalized product recommendations
Repeat-purchase reminders
Limited-time offers
Category-based promotions
Loyalty rewards
The business should focus on moving customers from occasional → returning → loyal behavior.

4. Subscription represents a retention opportunity
Finding: Subscription users demonstrate stronger retention behavior.

Business interpretation: Subscription status appears to be associated with stronger customer engagement.

Recommendation: Marketing should investigate opportunities to convert high-frequency and returning customers into subscribers.

Instead of promoting subscriptions equally to every customer, prioritize customers who already demonstrate repeated purchasing behavior.

5. Younger customers show higher transaction spending
Finding: Younger age groups spend more per transaction.

Business interpretation: Younger customers may represent an attractive target for campaigns focused on higher-value purchases.

Recommendation: Test targeted promotions, personalized product recommendations, and digital-first campaigns for younger customer groups while monitoring whether increased transaction value translates into stronger long-term customer value.

6. Customer satisfaction is generally positive
Finding: The average customer rating is approximately 3.75/5.

Business interpretation: Overall satisfaction appears reasonably positive, but there is still room to improve the customer experience.

Recommendation: Analyze lower-rated products and categories separately to identify recurring issues in product quality, fulfillment, or customer expectations.

💡 Business Recommendations
Based on the analysis, the following actions should be prioritized.

1. Retain high-value customers
Loyal customers are responsible for a significant share of revenue.

Action:

Introduce loyalty-focused campaigns
Offer personalized promotions
Reward repeat purchases
Provide early access to selected products or offers
Goal: Reduce customer churn and protect recurring revenue.

2. Convert returning customers into loyal customers
Returning customers already demonstrate some level of engagement.

Action:

Identify customers with increasing purchase frequency
Provide targeted incentives for the next purchase
Recommend products based on previous purchases
Create milestone-based loyalty rewards
Goal: Increase customer lifetime value by encouraging repeat purchases.

3. Increase subscription adoption
Subscribers show stronger retention behavior.

Action:

Target frequent and returning customers with subscription offers rather than using a broad, untargeted campaign.

Goal: Convert existing engaged customers into subscribers and strengthen retention.

4. Protect high-performing categories
Clothing is currently the strongest category.

Action:

Monitor demand
Maintain availability of high-performing products
Use best-selling items in promotional campaigns
Explore cross-selling opportunities with related products
Goal: Protect the category's contribution to revenue while identifying opportunities for additional basket value.

5. Use purchase frequency for customer targeting
Purchase frequency provides a useful signal for customer value.

Action:

Create marketing strategies based on customer behavior:

Customer Type	Recommended Strategy
New	Welcome campaigns and first-repeat incentives
Returning	Personalized recommendations and targeted offers
Loyal	Retention, loyalty rewards and exclusive benefits

Goal: Move customers progressively toward higher-value behavior.

6. Investigate lower-rated experiences
The average rating is positive, but the remaining gap provides an opportunity.

Action:

Analyze low-rated products by category and identify whether dissatisfaction is concentrated around specific products or customer groups.

Goal: Improve customer experience and reduce potential reasons for repeat-purchase decline.

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

📊 Project Deliverables
File	Description
customer_shopping_behavior.csv	Raw customer shopping dataset
python_sql_pbi__end_to_end project.ipynb	Python analysis and preprocessing
sql_queries.sql	SQL business analysis
CustomerBehavior_Analysis_SQL_Python_PBI.pbix	Power BI dashboard
dashboard_overview.png	Dashboard overview
product_performance.png	Product performance analysis
customer_segmentation.png	Customer segmentation
key_insights.png	Key business insights

🚀 How to Explore the Project
Step 1 — Explore the dataset
Review:

customer_shopping_behavior.csv

Step 2 — Review the Python analysis
Open the Jupyter notebook to understand:

Data quality checks
Missing-value treatment
Exploratory analysis
Data preparation
Step 3 — Review the SQL analysis
Open:

sql_queries.sql

Focus on the CTEs, window functions, aggregations, and segmentation logic.

Step 4 — Explore the Power BI dashboard
Open:

CustomerBehavior_Analysis_SQL_Python_PBI.pbix

Use the dashboard to explore the customer, product, revenue, and segmentation insights interactively.

🎯 Business Value
This project demonstrates how raw transactional data can be transformed into business decisions.

The analytical process moves from:

Data → Information → Insight → Recommendation

Rather than simply reporting that "Clothing is the top category," the analysis asks:

What does this mean for the business, and what should the business do next?

The resulting recommendations focus on:

Customer retention
Customer segmentation
Subscription conversion
Purchase-frequency growth
Product/category optimization
Customer experience
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
Business Intelligence
Power BI
KPI Development
Business Storytelling
Data-Driven Recommendations
👤 Author
Chandrashekar Sharma M

Data Analytics | Python | SQL | Power BI

GitHub: https://github.com/csmahi
LinkedIn: https://www.linkedin.com/in/chandrashekar-m-807267296/
⭐ Project Summary
Customer Shopping Behavior Analysis is an end-to-end analytics project that demonstrates the ability to transform customer transaction data into actionable business insights using Python, SQL, and Power BI.
