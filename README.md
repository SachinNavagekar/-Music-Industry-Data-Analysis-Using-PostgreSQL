# -Music-Industry-Data-Analysis-Using-PostgreSQL
This project focuses on analyzing music industry data using PostgreSQL to uncover insights about customer behavior, music genre trends, and revenue performance. The main objective was to understand which genres, artists, and cities drive the highest revenue and to identify key business opportunities for marketing and event planning.

# - 🧩 Tools & Technologies

Database: PostgreSQL

Techniques: SQL Joins, CTEs (Common Table Expressions), Aggregate Functions, Subqueries, and Data Filtering

Dataset: Music Store / Music Streaming Sales Data

# - 🔍 Business Objectives

Identify the most popular music genres based on listener data.

Determine the top customers and cities generating the highest revenue.

Analyze customer preferences and purchase patterns.

Provide data-driven insights for marketing, sales, and event strategy (e.g., promotional music festivals).

# - 🧠 Key SQL Analysis Performed

Genre Popularity Analysis

SELECT c.email, c.first_name, c.last_name, g.name AS genre
FROM customer c
JOIN invoice i ON c.customer_id = i.customer_id
JOIN invoice_line il ON i.invoice_id = il.invoice_id
JOIN track t ON il.track_id = t.track_id
JOIN genre g ON t.genre_id = g.genre_id
WHERE g.name = 'Rock'
ORDER BY c.email;


🔹 Finds all Rock music listeners, ordered alphabetically by email.

Top City by Revenue

WITH city_revenue AS (
  SELECT c.city, c.customer_id, c.first_name, 
         SUM(i.total) AS total_revenue
  FROM customer c
  JOIN invoice i ON c.customer_id = i.customer_id
  GROUP BY c.city, c.customer_id, c.first_name
)
SELECT city, SUM(total_revenue) AS total_city_revenue
FROM city_revenue
GROUP BY city
ORDER BY total_city_revenue DESC
LIMIT 1;


🔹 Identifies the city with the highest overall revenue.

Top Artists & Tracks by Sales
🔹 Determined which artists and songs generated the most income and how sales were distributed across regions.

Revenue Trends Over Time
🔹 Used date functions to analyze monthly and yearly sales growth, helping visualize business performance.

# - 📊 Insights & Outcomes

Rock and Pop genres were the most preferred among customers, contributing to the highest sales volume.

New York and London were the top-performing cities, making them ideal locations for promotional music festivals.

A small group of high-value customers accounted for a significant portion of total revenue.

PostgreSQL CTEs helped simplify complex multi-join queries and made analysis modular and efficient.

# - 🚀 Impact

This project demonstrates how data analytics with PostgreSQL can provide valuable insights into customer preferences and business performance in the music industry. The results can guide marketing campaigns, music event planning, and artist promotion strategies to maximize engagement and revenue.
