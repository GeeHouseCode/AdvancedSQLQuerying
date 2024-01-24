# Advanced Databases and SQL Querying (PORTFOLIO)
Practice to become better!!!

This repository contains portfolio of data science projects for the purpouse of self learnig and hobby.

## SQL VIEWS
#### Excercise 1. 
Create SQL VIEWS to check how many sellers we have in the United States (US).

An example solution:

```T-SQL
CREATE VIEW CustomUSView
AS
SELECT * FROM [AdventureWorks2012].[Sales].[SalesTerritory]
WHERE CountryRegionCode LIKE 'US'
```
The result of the above SQL Views is the following table.
```SQL
SELECT * FROM CustomUSView
```
![View_1](https://github.com/GeeHouseCode/AdvancedSQLQuerying/assets/110656951/c2b09409-d4d8-430b-9b92-ea4a0aabd8f8)

#### Excercise 2.
Create SQL Views showing the execution of sales quotas and bonuses earned for North America.
```T-SQL
CREATE VIEW SalesQuota
AS 
SELECT [Name], [Group], [SalesQuota], [Bonus]
FROM [Sales].[SalesTerritory] a INNER JOIN [Sales].[SalesPerson] b 
ON a.TerritoryID = b.TerritoryID
WHERE [Group] LIKE 'North America'
```
The result of the above SQL Views is the following table.
```SQL
SELECT * FROM SalesQuota
```
![View_2](https://github.com/GeeHouseCode/AdvancedSQLQuerying/assets/110656951/b9673cb4-18c2-47da-8ed3-01a8f52f2331)

#### Excercise 3.
The created SQL view will show which goods have been delivered and which have not.
```T-SQL
CREATE VIEW ShippedOrdersView 
AS
SELECT 
    OrderID,
    CustomerID,
    OrderDate,
    ShipName,
    CASE 
        WHEN ShippedDate IS NOT NULL THEN ShipCity
        ELSE 'NO DATA'
    END AS ShipCity,
    CASE 
        WHEN ShippedDate IS NOT NULL THEN ShipAddress
        ELSE 'NO DATA'
    END AS ShipAddress,
	CASE 
        WHEN ShippedDate IS NOT NULL THEN 'Delivered'
        ELSE 'Not delivered'
    END AS ShippedOrdersINF,
	ShippedDate
FROM 
    Northwind.dbo.Orders
```
The result of the above SQL Views is the following table.
```SQL
SELECT * FROM ShippedOrdersView
```
![View_3](https://github.com/GeeHouseCode/AdvancedSQLQuerying/assets/110656951/554aefa0-5b59-4201-98eb-32dc86152190)

#### Excercise 4.
The created view shows the products that are most often sold in a given region

!!! Handwritten version, not tested on the server :P "concept"
```T-SQL
CREATE VIEW MostSoldProductsByRegionView AS
SELECT
    r.RegionDescription,
    p.ProductName,
    COUNT(*) AS SalesCount
FROM
    Regions r
    INNER JOIN Territories t ON r.RegionID = t.RegionID
    INNER JOIN Employees e ON t.TerritoryID = e.TerritoryID
    INNER JOIN Orders o ON e.EmployeeID = o.EmployeeID
    INNER JOIN OrderDetails od ON o.OrderID = od.OrderID
    INNER JOIN Products p ON od.ProductID = p.ProductID
GROUP BY
    r.RegionDescription,
    p.ProductName
HAVING
    COUNT(*) = (
        SELECT
            MAX(SalesCount)
        FROM
            (
                SELECT
                    COUNT(*) AS SalesCount
                FROM
                    Regions r
                    INNER JOIN Territories t ON r.RegionID = t.RegionID
                    INNER JOIN Employees e ON t.TerritoryID = e.TerritoryID
                    INNER JOIN Orders o ON e.EmployeeID = o.EmployeeID
                    INNER JOIN OrderDetails od ON o.OrderID = od.OrderID
                    INNER JOIN Products p ON od.ProductID = p.ProductID
                WHERE
                    r.RegionDescription = MostSoldProductsByRegionView.RegionDescription
                GROUP BY
                    p.ProductName
            ) AS Temp
    )

```
