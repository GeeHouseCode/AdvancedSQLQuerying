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


