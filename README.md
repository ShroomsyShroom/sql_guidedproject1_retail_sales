<h1>SQL Retail Sales Analysis</h1>

<p>
This project is a guided SQL analysis focused on retail sales data.
It demonstrates database creation, data cleaning, exploratory data analysis,
and business-focused SQL querying using PostgreSQL.
</p>

<h2>Project Objective</h2>

<p>
The objective of this project is to analyze retail transaction data and answer
key business questions using structured SQL queries.
</p>

<p style="font-size:14px;">
The project emphasizes data preparation, handling missing values,
and applying analytical SQL concepts such as aggregations,
window functions, and common table expressions.
</p>

<h2>Tools Used</h2>

<p>
PostgreSQL (pgAdmin) is used for database management and SQL execution,
while Microsoft Excel is used for initial data inspection.
</p>

<h2>Project Workflow</h2>

<p>
The analysis follows a step-by-step workflow starting from data ingestion
to answering business-driven analytical questions.
</p>

<p style="font-size:14px;">
The workflow includes downloading the dataset, database setup,
table creation, data import, data cleaning, exploration, and analysis.
</p>

<h2>Database Setup</h2>

<p>
A new PostgreSQL database is created to store and analyze retail sales data.
</p>

<pre><code>
CREATE DATABASE sql_project_p1;
</code></pre>

<h2>Table Creation</h2>

<p>
A single table is created to store all transaction-level retail sales data.
Date fields are formatted using the YYYY-MM-DD standard.
</p>

<pre><code>
DROP TABLE IF EXISTS retail_sales;

CREATE TABLE retail_sales
(
    transactions_id INT PRIMARY KEY,
    sale_date DATE,
    sale_time TIME,
    customer_id INT,
    gender VARCHAR(15),
    age INT,
    category VARCHAR(15),
    quantity INT,
    price_per_unit FLOAT,
    cogs FLOAT,
    total_sale FLOAT
);
</code></pre>

<h2>Data Import and Validation</h2>

<p>
The dataset is imported into the table using pgAdmin’s import feature.
Column headers are disabled during import as they are already defined.
</p>

<p style="font-size:14px;">
After import, row counts are validated against the CSV file
and any errors are reviewed using the View Processes option.
</p>

<h2>Handling Missing Values</h2>

<p>
Null values are identified to ensure data quality before analysis.
</p>

<pre><code>
SELECT * FROM retail_sales
WHERE
    transactions_id IS NULL
    OR sale_date IS NULL
    OR sale_time IS NULL
    OR customer_id IS NULL
    OR gender IS NULL
    OR age IS NULL
    OR category IS NULL
    OR quantity IS NULL
    OR cogs IS NULL
    OR total_sale IS NULL;
</code></pre>

<p style="font-size:14px;">
Records containing critical missing values are removed to maintain
data consistency and analytical accuracy.
</p>

<pre><code>
DELETE FROM retail_sales
WHERE
    transactions_id IS NULL
    OR sale_date IS NULL
    OR sale_time IS NULL
    OR gender IS NULL
    OR category IS NULL
    OR quantity IS NULL
    OR cogs IS NULL
    OR total_sale IS NULL;
</code></pre>

<h2>Exploratory Data Analysis</h2>

<p>
Initial exploration is performed to understand the scale and structure
of the dataset.
</p>

<p style="font-size:14px;">
This includes counting total sales, identifying unique customers,
and listing distinct product categories.
</p>

<pre><code>
SELECT COUNT(*) AS total_sales FROM retail_sales;
</code></pre>

<pre><code>
SELECT COUNT(DISTINCT customer_id) AS total_customers FROM retail_sales;
</code></pre>

<pre><code>
SELECT DISTINCT category FROM retail_sales;
</code></pre>

<h2>Business Questions and Analysis</h2>

<p>
SQL queries are written to answer common retail business questions
related to sales performance, customer behavior, and trends.
</p>

<p style="font-size:14px;">
The analysis covers date-based filtering, category performance,
customer demographics, transaction thresholds,
and time-based sales patterns.
</p>

<h3>Examples of Business Analysis</h3>

<p style="font-size:14px;">
Retrieve sales from a specific date, analyze category-wise performance,
calculate average customer age by category, identify high-value transactions,
and determine top customers based on total spending.
</p>

<h2>Advanced SQL Concepts Used</h2>

<p>
The project applies intermediate SQL concepts to extract deeper insights.
</p>

<p style="font-size:14px;">
These include window functions for ranking,
date extraction for monthly analysis,
and Common Table Expressions (CTEs) for shift-based sales segmentation.
</p>

<h2>Shift-Based Sales Analysis</h2>

<p>
Sales are categorized into Morning, Afternoon, and Evening shifts
based on transaction time.
</p>

<p style="font-size:14px;">
This helps identify ordering patterns across different times of the day
and supports operational planning.
</p>

<h2>Project Outcome</h2>

<p>
The project successfully demonstrates a complete SQL-based
retail sales analysis workflow.
</p>

<p style="font-size:14px;">
It highlights practical SQL usage for data cleaning,
exploratory analysis, and answering real-world business questions.
</p>
