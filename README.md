
                                                           
                                                           
                                                           
                                                           🛒-Walmart-Sales-Data-Analysis-using-SQL

             This project presents an end-to-end SQL-based data analysis of Walmart Sales Data. The goal was
             to clean, transform, and extract insights from a retail transaction dataset using MySQL. It includes
             data preprocessing, feature engineering, and exploratory data analysis (EDA) to draw valuable business insights


       ❓ Problem Statement

             Walmart wants to understand customer behavior and product performance by analyzing transactional data. Key goals are:

             Identify revenue trends across time and product categories

             Understand customer types, preferences, and demographics

             Analyze product performance and city/branch-level contributions

             Create new features like time_of_day, day_name, and month_name for better time-based insights


       📂 Raw Data Details
             Source: The dataset used in this project is a publicly available CSV file named WalmartSalesData.csv.

<img width="958" height="475" alt="Screenshot 2025-07-27 164112" src="https://github.com/user-attachments/assets/a44bcb99-4a54-4e2d-82fa-c519c2810934" />



             Dataset Size: Contains 1,000+ transaction records with details across multiple retail branches of Walmart.

       📥 Data Access & Upload
             The dataset was loaded into the MySQL database using the following command:

             LOAD DATA LOCAL INFILE 
             'WalmartSalesData.csv'
             INTO TABLE sales
             FIELDS TERMINATED BY ','
             ENCLOSED BY '"'
             LINES TERMINATED BY '\n'
             IGNORE 1 ROWS;

       🧾 Data Preparation
             Table Name: sales
             Data Source: WalmartSalesData.csv (loaded via LOAD DATA LOCAL INFILE)
             Columns:

             Invoice ID, Branch, City, Customer Type, Gender

             Product Line, Unit Price, Quantity, VAT, Total

             Date, Time, Payment Method, COGS, Gross Income, Rating



       🧪 Feature Engineering
             Three additional columns were engineered:

Time of Day

             ALTER TABLE sales ADD COLUMN time_of_day VARCHAR(20);
             UPDATE sales
             SET time_of_day = (
               CASE 
                 WHEN time BETWEEN '00:00:00' AND '12:00:00' THEN 'Morning'
                 WHEN time BETWEEN '12:01:00' AND '16:00:00' THEN 'Afternoon'
                 ELSE 'Evening' 
               END
             );


       Day Name
       
             ALTER TABLE sales ADD COLUMN day_name VARCHAR(10);
             UPDATE sales SET day_name = DAYNAME(date);


       Month Name
       
             ALTER TABLE sales ADD COLUMN month_name VARCHAR(10);
             UPDATE sales SET month_name = MONTHNAME(date);


       📦 Product Analysis


Q1. Most common payment method?

             SELECT payment, COUNT(*) AS count FROM sales 
             GROUP BY payment ORDER BY count DESC LIMIT 1;


Q2. Total revenue by month?

             SELECT month_name, SUM(total) AS total_revenue FROM sales 
             GROUP BY month_name ORDER BY total_revenue DESC;


Q3. Highest revenue product line?

             SELECT product_line, SUM(total) AS total_revenue FROM sales 
             GROUP BY product_line ORDER BY total_revenue DESC LIMIT 1;



Q4. Highest revenue city?

             SELECT city, SUM(total) AS total_revenue FROM sales 
             GROUP BY city ORDER BY total_revenue DESC LIMIT 1;


Q5. Product line with highest VAT?

             SELECT product_line, SUM(vat) AS VAT FROM sales 
             GROUP BY product_line ORDER BY VAT DESC LIMIT 1;



       💰 Sales Analysis
Q1. Sales per weekday per time of day?

             SELECT day_name, time_of_day, COUNT(*) AS total_sales 
             FROM sales 
             WHERE day_name NOT IN ('Saturday', 'Sunday') 
             GROUP BY day_name, time_of_day;


Q2. Which customer type generates highest revenue?

             SELECT customer_type, SUM(total) AS total_sales 
             FROM sales GROUP BY customer_type ORDER BY total_sales DESC LIMIT 1;

Q3. Which gender dominates the customer base?

             SELECT gender, COUNT(*) AS total FROM sales 
             GROUP BY gender ORDER BY total DESC LIMIT 1;


Q4. Gender distribution per branch?

              SELECT branch, gender, COUNT(*) AS count 
             FROM sales GROUP BY branch, gender;


       📚 Learnings
       
             Advanced SQL querying for retail analytics

             Feature engineering using SQL

             Grouping and filtering using GROUP BY, HAVING, and CASE

             Business insights derivation from transactional data



       📜 License
       
             This project is open-source and free to use under the MIT License.



       ✅ Summary
       
             This Walmart sales analysis project showcases how SQL can be leveraged to perform end-to-end business analysis. It includes:

             Data ingestion, transformation, and enrichment

             More than 30 real business queries

             Clean, well-documented SQL code

             Actionable insights ready for stakeholder presentation
