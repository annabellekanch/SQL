# Common Table Expressions
## Table Columns 
| ProductID   | StartDate  | EndDate   | ListPrice  | ModifiedDate  |
|:-:|:-:|:-:|:-:|:-:|

## CTE 
CTE to join ProductCostHistory Table & ProductListPriceHistory Table and return the Average Standard Cost & Average List Price partitioned by the ProductID for each product where the Standard Cost and List Price are less then 10. 
```SQL
WITH CTE_Product as 
  (
	SELECT plph.ProductID, plph.StartDate, plph.EndDate,
	  AVG(StandardCost) OVER (PARTITION BY plph.ProductID) as AvgStandardCost,  
	  AVG(ListPrice) OVER (PARTITION BY plph.ProductID) as AvgListPrice
	  FROM [AdventureWorks2019].[Production].[ProductListPriceHistory] plph 
	  JOIN [AdventureWorks2019].[Production].[ProductCostHistory] pch
		ON plph.ProductID = pch.ProductID
	  WHERE StandardCost < 10 AND ListPrice < 10
	  GROUP BY plph.ProductID, plph.StartDate, plph.EndDate, plph.ListPrice, StandardCost 
	  
	)
SELECT *
FROM CTE_Product
```
### Query Results
| ProductID | StartDate               | EndDate                 | AvgStandardCost | AvgListPrice |
|-----------|-------------------------|-------------------------|-----------------|--------------|
| 709       | 2011-05-31 00:00:00.000 | 2012-05-29 00:00:00.000 | 3.3963          | 9.50         |
| 710       | 2011-05-31 00:00:00.000 | 2012-05-29 00:00:00.000 | 3.3963          | 9.50         |
| 712       | 2011-05-31 00:00:00.000 | 2012-05-29 00:00:00.000 | 5.9524          | 8.7594       |
| 712       | 2011-05-31 00:00:00.000 | 2012-05-29 00:00:00.000 | 5.9524          | 8.7594       |
| 712       | 2011-05-31 00:00:00.000 | 2012-05-29 00:00:00.000 | 5.9524          | 8.7594       |
| 712       | 2012-05-30 00:00:00.000 | 2013-05-29 00:00:00.000 | 5.9524          | 8.7594       |
| 712       | 2012-05-30 00:00:00.000 | 2013-05-29 00:00:00.000 | 5.9524          | 8.7594       |
| 712       | 2012-05-30 00:00:00.000 | 2013-05-29 00:00:00.000 | 5.9524          | 8.7594       |
| 712       | 2013-05-30 00:00:00.000 | NULL                    | 5.9524          | 8.7594       |
| 712       | 2013-05-30 00:00:00.000 | NULL                    | 5.9524          | 8.7594       |
| 712       | 2013-05-30 00:00:00.000 | NULL                    | 5.9524          | 8.7594       |
| 870       | 2013-05-30 00:00:00.000 | NULL                    | 1.8663          | 4.99         |
| 871       | 2013-05-30 00:00:00.000 | NULL                    | 3.7363          | 9.99         |
| 872       | 2013-05-30 00:00:00.000 | NULL                    | 3.3623          | 8.99         |
| 873       | 2013-05-30 00:00:00.000 | NULL                    | 0.8565          | 2.29         |
| 874       | 2013-05-30 00:00:00.000 | NULL                    | 3.3623          | 8.99         |
| 875       | 2013-05-30 00:00:00.000 | NULL                    | 3.3623          | 8.99         |
| 877       | 2013-05-30 00:00:00.000 | NULL                    | 2.9733          | 7.95         |
| 921       | 2013-05-30 00:00:00.000 | NULL                    | 1.8663          | 4.99         |
| 922       | 2013-05-30 00:00:00.000 | NULL                    | 1.4923          | 3.99         |
| 923       | 2013-05-30 00:00:00.000 | NULL                    | 1.8663          | 4.99         |
