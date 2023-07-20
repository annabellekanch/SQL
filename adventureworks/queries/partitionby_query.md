# PARTITION BY query performed on ProductListPriceHistory
## Table Columns
| ProductID  | StartDate  | EndDate  | ListPrice |  ModifiedDate  |
|:-:|:-:|:-:|:-:|:-:|

1. Find the average, min, and max list price for each product
## Finding average, min, and max list price
```SQL
 SELECT Top(15) ProductID,
		AVG(ListPrice) AS AverageListPrice,
		MIN(ListPrice) AS MinListPrice,
		MAX(ListPrice) AS MaxListPrice
  FROM [AdventureWorks2019].[Production].[ProductListPriceHistory]
  GROUP BY ProductID
```
### Query Results
