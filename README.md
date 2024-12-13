# U.S. Baby Names Analysis Using SQL

### Project Overview

This project analyzes baby names from U.S. Social Security card applications spanning three decades (1980–2010). By leveraging SQL, I examined trends in name popularity by year, state, and gender to uncover meaningful insights into naming conventions across the United States. The dataset provides a rich view of cultural, regional, and temporal influences on baby naming practices.

### Objectives

The primary goal of this analysis is to explore how naming trends evolve over time and reveal interesting patterns in the data. Key questions addressed include:

Most Popular Names Over Time: What are the most popular baby names for each decade? How do they change over time?
Names with Significant Trends: Which baby names experienced the largest jumps or drops in popularity?
Gender-Specific Trends: Are there distinct patterns in names given to boys, girls, or both? How have unisex names evolved?

### Key Analysis Highlights
Decade-Wise Popularity: Identified the top names for each decade, highlighting names that dominated across states and genders.
Trend Analysis: Analyzed names with sharp rises or falls, identifying factors like pop culture influences or historical events.
Gender Trends: Explored the distribution of names by gender and tracked the rise of unisex names over time.

### Tools and Technologies
SQL: For data extraction, aggregation, and analysis.
Database: Hosted and queried the dataset using PostgreSQL

### Dataset
The dataset includes baby names registered in the U.S. from 1980 to 2010, sourced from the Social Security Administration (SSA). It comprises fields like name, gender, year, state, and frequency.

### Sample SQL Queries
Here are examples of queries used during the analysis:

Most Popular Names by Decade:

SELECT name, gender, SUM(count) AS total_count, FLOOR(year / 10) * 10 AS decade
FROM baby_names
GROUP BY name, gender, decade
ORDER BY decade, total_count DESC;

Names with Largest Trend Shifts:

WITH ranked_names AS (
    SELECT name, year, count,
           RANK() OVER (PARTITION BY name ORDER BY year) AS rank
    FROM baby_names
)
SELECT name, MAX(count) - MIN(count) AS popularity_change
FROM ranked_names
GROUP BY name
ORDER BY popularity_change DESC;

Gender-Specific Analysis:

SELECT name, gender, COUNT(DISTINCT year) AS years_popular
FROM baby_names
GROUP BY name, gender
HAVING COUNT(DISTINCT year) > 5
ORDER BY years_popular DESC;

### Insights

Dominant Names: Names like “Michael” and “Jessica” dominated multiple decades, but newer trends emerged post-2000.
Trend Breakers: Names like “Aiden” and “Isabella” saw meteoric rises, likely influenced by popular culture.
Gender-Neutral Names: Names like “Taylor” and “Jordan” gained traction as unisex names, reflecting broader social changes.

### Future Directions
This analysis can be extended by:

Comparing state-level trends to identify regional preferences.
Exploring correlations between baby names and external factors like movies, celebrity influence, or historical events.
Building predictive models to forecast future naming trends.

### Repository Contents
SQL Scripts: Query files used for data analysis.



