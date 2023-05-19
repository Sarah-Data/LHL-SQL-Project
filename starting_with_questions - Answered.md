Answer the following questions and provide the SQL queries used to find the answer.

    
**Question 1: Which cities and countries have the highest level of transaction revenues on the site?**


SQL Queries:```
SELECT country, city, SUM(totaltransactionrevenue)total_revenue
FROM all_sessions_clean
GROUP BY 1,2
ORDER BY 3 DESC
LIMIT 10
```

Answer:image.png



**Question 2: What is the average number of products ordered from visitors in each city and country?**


SQL Queries:```
SELECT  a_s.country,a_s.city,
CAST(AVG(p.orderedquantity) AS NUMERIC(10,2))average_products_ordered
FROM all_sessions_clean a_s
JOIN products_clean p ON p.sku = a_s.productsku
WHERE p.orderedquantity >0
GROUP BY 1,2
ORDER BY 3 DESC
LIMIT 10
```



Answer:image.png





**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


SQL Queries:```
 SELECT  a_s.country,a_s.city,a_s.v2productcategory, p.name, SUM(p.orderedquantity) products_ordered
FROM all_sessions_clean a_s
JOIN products_clean p ON p.sku = a_s.productsku
WHERE p.orderedquantity >0
GROUP BY 1,2,3,4
ORDER BY 5 DESC
LIMIT 10
```



Answer:image.png





**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:```
SELECT a.country, a.city, c.name,SUM(b.units_sold)Top_Products_By_Units
FROM all_sessions_clean a
JOIN analytics_dup b USING(fullvisitorid)
JOIN products_clean c ON c.sku = a.productsku
GROUP BY 1,2,3
ORDER BY 4 DESC
LIMIT 10
```




Answer:image.png





**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries: ```
SELECT a.city,a.timeonsite,b.channelgrouping,c.sentimentscore,SUM(a.totaltransactionrevenue) Total_Revenue
from
all_sessions_clean a
JOIN analytics_dup b USING (fullvisitorid)
JOIN products_clean c ON c.sku = a.productsku
where totaltransactionrevenue >0
GROUP BY 1,2,3,4
ORDER BY 5 DESC
LIMIT 10
```



Answer: image.png







