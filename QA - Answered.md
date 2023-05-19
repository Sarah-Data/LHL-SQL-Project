**What are your risk areas? Identify and describe them.**

Though i found some duplicate and irrelevant attibutes, i did not want to alter the table structure, i created new tables as all_sessions_clean, analytics_clean and products_clean and did some data cleaning by changing null values in numerical fields to 0 and categorical fields to N/A.    

Negative values in units_sold was zerorized and astronomical values of the unit_price regularized by dividing the column by 1,000,000 as hinted.
For consistency, rows with empty currency as imputed with 'USD' which ireckon is the standard reporting currency.   

After cleaning the data, i found that the analytics table of over 4.5m records have duplicate reocrds and i created another table called analytics_dup and moved the unique records into it from the existing analytics_clean table
```
CREATE TABLE analytics_dup AS 
SELECT DISTINCT * FROM analytics_clean
```
Regarding building relationships, the all_sessions and analytics table do not have uniqie identifiers and i tried creating composite keys using a combination of multiple records (fullvisitorid and visitid)  which still was not unique.

There is a total of 293,537 units sold in the analytics table out of which 230,436 is without revenue. It would be nice to know if they are promo products and create a separate table the displays the attributes (promo_units) for a smooth relationship modelling and better analysis.


**QA Process:
Describe your QA process and include the SQL queries used to execute it.**

1. **Count Validation** - Reurns the number of productskuin the sales report table that is not in the all_sessions_clean_table
```
SELECT DISTINCT COUNT (productsku) 
FROM sales_report
WHERE productsku NOT IN (SELECT productsku FROM all_sessions_clean)
```
2. **Sum Validation** 
```SELECT SUM(units_sold) from analytics_dup```  

3. **Average Validation**  
4. 
5. **Min and Max Validation** - Revealed a negative value in the units_sold which was changed to 0
```
SELECT MIN(units_sold) from analytics
```
5. **Existence Validation** - Returns the matching records of product sku in the sales report and all_sessions_clean tables
```
SELECT *
FROM sales_report a 
WHERE EXISTS (
    SELECT *
    FROM all_sessions_clean b
    WHERE b.productsku = a.productsku
);
```
OR
```
SELECT DISTINCT COUNT (productsku) 
FROM sales_report
WHERE productsku NOT IN (SELECT productsku FROM all_sessions_clean)
```

