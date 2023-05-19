# Final-Project-Transforming-and-Analyzing-Data-with-SQL

## Project/Goals
The project requires that i set up a database named "E-commerce" on Postgres and import 5 tables to analyze and develop insights.
## Process
Data importing
 - Identify data types for each column
 - Create tables
 - Import data from CSV
Data Cleaning

Data Validation
 - Check for Null values
 - Check for outliers (negative and astronomical values)
 - Validate all attributes for integrity and consistency

Data Cleaning
 - Remove empty column
 - Remove duplicate columns
 - Remove duplicate records

## Results
The data is able to show visitor behaviou, the channels that attracted more sales, the conversion rate per click on the website, the country and city that contributes most to the company's topline(revenue), the products that revenue-drivers.
These were analyzed using aggregations like SUM(), COUNT(), AVG() and GROUP BY() and ORDER BY()
ROW_NUMBER() PARTION BY was also used to get the duplicate records in the analytics table in order to provide accurate and reliable insights

## Challenges 
- The tables were not normalized and relationship was hard to recognize
- There are lots of Null values in the numerical fields that were turned to 0 but which which makes descriptive analysis weird especially when using average function


## Future Goals
Further cleaning
Normalizing the tables
Developing unique identifiers to form 1:1 or One:Many relational models
