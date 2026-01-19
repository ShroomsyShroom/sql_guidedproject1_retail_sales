<h1>Retail Sales Analysis Project</h1>

<p>This project involves a comprehensive analysis of retail sales data to uncover customer purchasing patterns, category performance, and sales trends. The workflow covers the entire data pipeline, from database schema creation and data cleaning to complex analytical querying.</p>

<h2>Project Workflow</h2>

<h3>1. Data Preparation and Database Setup</h3> <p>The process begins by preparing the raw data in CSV format and establishing a structured environment in PostgreSQL (pgAdmin).</p>

<ul> <li>Download the retail sales dataset as a CSV file.</li> <li>Identify column names and data types from the source file.</li> <li>Create a new database in pgAdmin named <code>sql_project_p1</code>.</li> </ul>

<pre> -- SQL Retail Sales Analysis - P1 CREATE DATABASE sql_project_p1; </pre>

<h3>2. Schema Definition</h3> <p>A table is defined to store the retail transactions with specific constraints and data types to ensure consistency, particularly for dates and monetary values.</p>

<pre> -- Creating the retail sales table DROP TABLE IF EXISTS retail_sales; CREATE TABLE retail_sales ( transactions_id INT PRIMARY KEY, sale_date DATE, sale_time TIME, customer_id INT, gender VARCHAR(15), age INT, category VARCHAR(15),

quantity INT, price_per_unit FLOAT,

cogs FLOAT, total_sale FLOAT ); </pre>

<h3>3. Data Ingestion and Verification</h3> <p>Data is imported into the <code>retail_sales</code> table. It is crucial to disable the "Headers" option during import since the table structure is already defined. Post-import, the record count is verified against the source file using the following command:</p>

<pre>SELECT COUNT(*) FROM retail_sales;</pre>

<h3>4. Data Cleaning</h3> <p>To ensure the accuracy of the analysis, the dataset is checked for null values. Any records with missing critical information are identified and removed.</p>

<pre> -- Identifying records with NULL values SELECT * FROM retail_sales WHERE transactions_id IS NULL OR sale_date IS NULL OR sale_time IS NULL OR customer_id IS NULL OR gender IS NULL OR category IS NULL OR quantity IS NULL OR cogs IS NULL OR total_sale IS NULL;

-- Deleting NULL records DELETE FROM retail_sales WHERE transactions_id IS NULL OR sale_date IS NULL OR sale_time IS NULL OR gender IS NULL OR category IS NULL OR quantity IS NULL OR cogs IS NULL OR total_sale IS NULL; </pre>

<h2>Data Exploration and Basic Insights</h2> <p>Initial exploration helps understand the scale and diversity of the business operations.</p>

<ul> <li><strong>Total Sales Count:</strong> <code>SELECT COUNT(*) as total_sale FROM retail_sales;</code></li> <li><strong>Unique Customer Base:</strong> <code>SELECT COUNT(DISTINCT customer_id) as total_unique_customers FROM retail_sales;</code></li> <li><strong>Product Categories:</strong> <code>SELECT DISTINCT category FROM retail_sales;</code></li> </ul>

<h2>Business Analysis (SQL Queries)</h2>

<h3>Category and Date Filtering</h3> <p>Retrieving transactions for specific timeframes or product categories, such as clothing sales in November 2022 where quantities exceeded 10.</p>

<pre> SELECT category, SUM(quantity) FROM retail_sales WHERE category = 'Clothing' AND TO_CHAR(sale_date, 'YYYY-MM') = '2022-11' GROUP BY 1; </pre>

<h3>Category Performance</h3> <p>Calculating total sales and order counts per category to identify the highest revenue generators.</p>

<pre> SELECT category, SUM(total_sale) as net_sale, COUNT(*) as total_orders FROM retail_sales GROUP BY 1; </pre>

<h3>Customer Demographics</h3> <p>Analyzing the average age of customers in specific segments, like the 'Beauty' category, to understand target audiences.</p>

<pre> SELECT ROUND(AVG(age), 2) as Average_age FROM retail_sales WHERE category = 'Beauty'; </pre>

<h3>Advanced Time-Series Analysis</h3> <p>Using Window Functions (RANK) to identify the best-selling month for each year based on average sales.</p>

<pre> SELECT year, month, avg_sale FROM ( SELECT EXTRACT(YEAR FROM sale_date) as year, EXTRACT(MONTH FROM sale_date) as month, AVG(total_sale) as avg_sale, RANK() OVER(PARTITION BY EXTRACT(YEAR FROM sale_date) ORDER BY AVG(total_sale) DESC) as rank FROM retail_sales GROUP BY 1, 2 ) as t1 WHERE rank = 1; </pre>

<h3>Shift Analysis</h3> <p>Categorizing transactions into time-based shifts (Morning, Afternoon, Evening) using Common Table Expressions (CTE) and CASE statements.</p>

<pre> WITH hourly_sale AS ( SELECT , CASE WHEN EXTRACT(HOUR FROM sale_time) < 12 THEN 'Morning' WHEN EXTRACT(HOUR FROM sale_time) BETWEEN 12 AND 17 THEN 'Afternoon' ELSE 'Evening' END as shift FROM retail_sales ) SELECT shift, COUNT() AS total_orders FROM hourly_sale GROUP BY shift; </pre>

<h2>Conclusion</h2> <p>This project successfully demonstrates the use of SQL for data cleaning, transformation, and complex business logic. The insights generated regarding customer shifts, high-value categories, and monthly performance provide a solid foundation for data-driven retail strategies.</p>
