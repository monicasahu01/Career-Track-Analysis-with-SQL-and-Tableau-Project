# Career-Track-Analysis-with-SQL-and-Tableau-Project
Exploring Student Enrollments and Completions in Data-Related Career Tracks 

Project Overview

The goal of this project is to perform an in-depth analysis of career tracks using SQL for data querying and Tableau for data visualization. By analyzing career progression data, we aim to uncover trends, patterns, and insights that can inform career development strategies and organizational policies.

Project Steps
Data Collection

Source: Obtain career track data from internal HR databases or publicly available datasets.
Format: Ensure the data is in a suitable format for analysis (e.g., CSV, Excel, SQL database).
Data Preparation

Cleaning: Use SQL to clean the data. This includes handling missing values, correcting inconsistencies, and normalizing data.
Transformation: Transform the data into a format suitable for analysis. Create necessary tables and relationships.

Data Analysis with SQL

Career Path Identification: 
Identify distinct career paths by querying job titles, departments, and transitions.
Tenure Analysis: Calculate average tenure in each role and department.
Promotion Patterns: Analyze the frequency and timing of promotions.
Attrition Rates: Determine attrition rates for different roles and departments.
Visualization with Tableau

Setup: 
Connect Tableau to the SQL database.

Dashboard Creation:
Career Path Visualization: Create flow diagrams showing common career paths.
Tenure and Promotion Analysis: Use bar charts, histograms, and scatter plots to visualize tenure and promotion patterns.
Attrition Analysis: Create heat maps or other relevant visualizations to show attrition rates.
Interactivity: Implement filters and interactive elements to allow users to explore the data.
Reporting and Insights

Summary Report: 
Compile a summary report detailing key findings and insights.
Recommendations: Provide actionable recommendations based on the analysis.
SQL Queries

Below are some example SQL queries for each analysis step:

Career Path Identification

sql code

SELECT employee_id, job_title, department, start_date, end_date
FROM career_tracks
ORDER BY employee_id, start_date;
Tenure Analysis

sql code

SELECT job_title, department, AVG(DATEDIFF(end_date, start_date)) AS avg_tenure
FROM career_tracks
GROUP BY job_title, department;
Promotion Patterns

sql code

WITH promotion_cte AS (
    SELECT employee_id, job_title, 
           LAG(job_title) OVER (PARTITION BY employee_id ORDER BY start_date) AS previous_job_title,
           start_date
    FROM career_tracks
)
SELECT previous_job_title, job_title, COUNT(*) AS promotion_count
FROM promotion_cte
WHERE previous_job_title IS NOT NULL
GROUP BY previous_job_title, job_title
ORDER BY promotion_count DESC;
Attrition Rates

sql code

SELECT department, job_title, COUNT(*) AS num_employees,
       SUM(CASE WHEN end_date IS NOT NULL THEN 1 ELSE 0 END) AS num_attrition,
       (SUM(CASE WHEN end_date IS NOT NULL THEN 1 ELSE 0 END) / COUNT(*)) * 100 AS attrition_rate
FROM career_tracks
GROUP BY department, job_title;
Tableau Dashboards
Career Path Visualization

Create Sankey diagrams or flow charts to illustrate the common career transitions.
Tenure and Promotion Analysis

Use bar charts to show average tenure per job title and department.
Scatter plots can illustrate the distribution of tenure before promotion.
Attrition Analysis

Heat maps to display attrition rates across different departments and roles.
Tools and Technologies
SQL: For data cleaning, transformation, and analysis.
Tableau: For data visualization and dashboard creation.
Excel/CSV: For initial data inspection and basic cleaning.
Deliverables
Cleaned and transformed dataset ready for analysis.
SQL scripts for data querying and analysis.
Tableau dashboards with interactive visualizations.
Summary report with key insights and recommendations.
Best Practices
Ensure data accuracy by validating SQL queries.
Use Tableau's interactive features to make dashboards user-friendly.

Regularly update the dataset and visualizations to reflect the most current data.
By following this approach, you will be able to provide comprehensive insights into career progression patterns within an organization, helping to inform strategic decisions in HR and talent management
