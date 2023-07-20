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
| ProductID | AverageListPrice | MinListPrice | MaxListPrice |
|-----------|------------------|--------------|--------------|
| 707       | 34.0928          | 33.6442      | 34.99        |
| 708       | 34.0928          | 33.6442      | 34.99        |
| 709       | 9.50             | 9.50         | 9.50         |
| 710       | 9.50             | 9.50         | 9.50         |
| 711       | 34.0928          | 33.6442      | 34.99        |
| 712       | 8.7594           | 8.6442       | 8.99         |
| 713       | 48.7082          | 48.0673      | 49.99        |
| 714       | 48.7082          | 48.0673      | 49.99        |
| 715       | 48.7082          | 48.0673      | 49.99        |
| 716       | 48.7082          | 48.0673      | 49.99        |
| 717       | 1332.1078        | 1263.4598    | 1431.50      |
| 718       | 1332.1078        | 1263.4598    | 1431.50      |
| 719       | 1332.1078        | 1263.4598    | 1431.50      |
| 720       | 1332.1078        | 1263.4598    | 1431.50      |
| 721       | 1332.1078        | 1263.4598    | 1431.50      |

2.Apply Partition By for ProductID
## Apply Partiotn By Query
```SQL
  SELECT Top(15) ProductID,
		AVG(ListPrice) OVER(PARTITION BY ProductID) AS AverageListPrice,
		MIN(ListPrice) OVER(PARTITION BY ProductID) AS MinListPrice,
		MAX(ListPrice) OVER(PARTITION BY ProductID) AS MaxListPrice
  FROM [AdventureWorks2019].[Production].[ProductListPriceHistory]
```
### Query Results
| ProductID | AverageListPrice | MinListPrice | MaxListPrice |
|-----------|------------------|--------------|--------------|
| 707       | 34.0928          | 33.6442      | 34.99        |
| 707       | 34.0928          | 33.6442      | 34.99        |
| 707       | 34.0928          | 33.6442      | 34.99        |
| 708       | 34.0928          | 33.6442      | 34.99        |
| 708       | 34.0928          | 33.6442      | 34.99        |
| 708       | 34.0928          | 33.6442      | 34.99        |
| 709       | 9.50             | 9.50         | 9.50         |
| 710       | 9.50             | 9.50         | 9.50         |
| 711       | 34.0928          | 33.6442      | 34.99        |
| 711       | 34.0928          | 33.6442      | 34.99        |
| 711       | 34.0928          | 33.6442      | 34.99        |
| 712       | 8.7594           | 8.6442       | 8.99         |
| 712       | 8.7594           | 8.6442       | 8.99         |
| 712       | 8.7594           | 8.6442       | 8.99         |
| 713       | 48.7082          | 48.0673      | 49.99        |
