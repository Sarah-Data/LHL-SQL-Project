Question 1: Find all duplicate records in the All_sessions and Analytics table

SQL Queries: 
```
WITH cte
AS
(
SELECT *,
       row_number() OVER (PARTITION BY fullVisitorId,	channelGrouping,
						  time,	country,	city,	totalTransactionRevenue,	transactions,
						  timeOnSite,	pageviews,	sessionQualityDim,	date,	visitId,	type,
						  productRefundAmount,	productQuantity,	productPrice,
						  productRevenue,	productSKU,	v2ProductName,	v2ProductCategory,
						  productVariant,	currencyCode,	itemQuantity,	itemRevenue,	
						  transactionRevenue,	transactionId,	pageTitle,	searchKeyword,	
						  pagePathLevel1,	eCommerceAction_type,	eCommerceAction_step,	
						  eCommerceAction_option

                          ORDER BY 1) rn
       FROM all_sessions_clean)
SELECT * from cte where rn >1
```
```
WITH cte2
AS
(
SELECT *,
       row_number() OVER (PARTITION BY visitNumber,	visitId,	visitStartTime,
						  date,	fullvisitorId,	userid,	channelGrouping,
						  socialEngagementType,	units_sold,	pageviews,	timeonsite,
						  bounces,	revenue,	unit_price
                          ORDER BY 3) rn
       FROM analytics_clean)
SELECT * FROM cte2
WHERE rn >1
```



**Answer**: There are no duplicatesin the all sessions table and there are over 2.5m duplicate records in the Analytics table.



Question 2: find the total number of unique visitors (`fullVisitorID`)

SQL Queries:
```
SELECT distinct(fullvisitorid)
FROM all_sessions_clean
```

**Answer**: There are 14,223 unique visitors based on fullvisitorid in the all_sessions table



Question 3: find the total number of unique visitors by channelgrouping

SQL Queries:
```
SELECT b.channelgrouping, COUNT(distinct a.fullvisitorid)Unique_Visitors
FROM all_sessions_clean a
FULL OUTER JOIN analytics_dup b USING(fullvisitorid)
GROUP BY 1
```

**Answer**: Although, there are over 14,000 unique visitors in the all_sessions table, there are no matching values for over 10,000 visitors ids in the analytics table
image.png



