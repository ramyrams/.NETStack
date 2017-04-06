
* [Questions About SQL Server Collations You Were Too Shy to Ask](https://www.simple-talk.com/sql/sql-development/questions-sql-server-collations-shy-ask/)


Ad hoc queries vs stored procedures vs Dynamic SQ
http://stackoverflow.com/questions/2934634/ad-hoc-queries-vs-stored-procedures-vs-dynamic-sql

https://www.simple-talk.com/sql/database-administration/retrieving-sql-server-query-execution-plans/

# SQL

## Table of Content
* [SELECT Statements](#select-statements)
* [SELECT JOIN](#select-join)
* [SELECT Group](#select-group)
* [SELECT Subquires](#select-subqueries)
* [SELECT Summarize Data](#select-summarize-data)
* [Common Problems & Solution](#select-solution)
* [SELECT Four Ranking Function](#four-ranking-function)
* [SELECT Analytic Functions](#analytic-functions)
* [Insert](#insert-statements)
* [Update Statements](#update-statements)
* [Delete Statements](#delete-statements)
* [UNION vs UNION ALL](#union-vs-union-all)
* [SELECT INTO](#select-into)
* [INSERT INTO SELECT](#insert-into-select-statement)
* [Common Table Expressions - CTE](#common-table-expressions---cte)
* [inbuild Functions](#inbuild-functions)
* [Index](#index)
* [CREATE Database](#create-database)
* [Tables](#Tables)
* [Stored Procedure](#stored-procedure)
* [Cursor](#cursor)
* [Views](#views)
* [Triggers](#triggers)
* [User Defined Functions](#user-defined-functions)
* [User Defined Types](#user-defined-types)
* [Error Handling](#error-handling)
* [Output Statements](#output-statements)
* [SET Statements](#set-statements)
* [Transcation Statements](#transcation-statements)
* [Manage Database Security](#Manage-Database-Security])
* [Configure](	)
* [System Stored Procedures](	)






http://stackoverflow.com/questions/139630/whats-the-difference-between-truncate-and-delete-in-sql
http://mangalpardeshi.blogspot.in/2009/07/delete-vs-truncate.html
http://www.webcodeexpert.com/2013/03/difference-between-delete-and-truncate.html



| Tables        | Are           | 
| ------------- |:-------------:| 
| != 	      	|Tests two expressions not being equal to each other. | 
| !>       		|Tests that the left condition is not greater than the expression to the right. | 
| !<       		|Tests that the right condition is not greater than the expression to the right. | 
| <       		|Tests the left condition as less than the right condition. | 
| <=       		|Tests the left condition as less than or equal to the right condition. | 
| <>       		|Tests two expressions not being equal to each other. | 
| =       		|Tests equality between two expressions. | 
| >       		|Tests the left condition being greater than the expression to the right. | 
| >=       		|Tests the left condition being greater than or equal to the expression to the right. | 
| ALL       	|When used with a comparison operator and subquery, retrieves rows if all retrieved values satisfy the search condition. | 
| ANY       	|When used with a comparison operator and subquery, retrieves rows if any retrieved values satisfy the search condition. | 
| BETWEEN       |Designates an inclusive range of values. Used with the AND clause between the beginning and ending values. | 
| CONTAINS      |Does a fuzzy search for words and phrases. | 
| ESCAPE        |Allows you to designate that a wildcard character be interpreted as a literal value instead.  | 
| EXISTS        |When used with a subquery, tests for the existence of rows in the subquery. |
| FREETEXT      |Searches character-based data for words using meaning, rather than literal values. |
| IN			|Provides an inclusive list of values for the search condition. |
| IS NOT NULL	|Evaluates whether the value is NOT NULL. |
| IS NULL       |Evaluates whether the value is NULL. |
| LIKE       	|Tests character string for pattern matching. |
| NOT BETWEEN   |Specifies a range of values NOT to include. Used with the AND clause between the beginning and ending values. |
| NOT IN       	|Provides a list of values for which NOT to return rows. |
| NOT LIKE      |Tests character string, excluding those with pattern matches. |
| SOME       	|When used with a comparison operator and subquery, retrieves rows if any retrieved values satisfy the search condition. |


| Wildcard      | Usage           | 
| ------------- |:-------------:| 
| % 			|Represents a string of zero or more characters | 
| _ 			|Represents a single character | 
| [] 			|Specifies a single character, from a selected range or list | 
| [^] 			|Specifies a single character not within the specified range | 



## SELECT Statements
**Logical Processing Order of the SELECT statement.**
1. FROM
2. ON
3. JOIN
4. WHERE
5. GROUP BY
6. WITH CUDE or WITH ROLLUP
7. HAVING
8. SELECT
9. DISTINCT
10. ORDER BY
11. TOP


``` sql 
--Simple One
SELECT * FROM Production.Product 

SELECT 
p.Name AS ProductName, -- a column heading is added.
NonDiscountSales = (OrderQty * UnitPrice) -- Calculated columns
Name, ProductNumber, ListPrice AS Price
FROM Production.Product AS p    -- Alternate way.
WHERE ProductLine = 'R' --Filter rows 


-- Select column, order by and where
SELECT * FROM Customers
WHERE (Country = 'Mexico' OR CustomerID >= 1)
AND (City <> 'Berlin' OR City LIKE '%s');
AND CustomerID BETWEEN 10 AND 100
AND City IN ('Paris','London');
OR City LIKE 'L_n_on';
OR City LIKE '_erlin';
OR City LIKE '[bsp]%'; -- City starting with "b", "s", or "p":
OR City LIKE '[a-c]%';
OR City '[!bsp]%';
ORDER BY Country ASC, CustomerName DESC;


--A. Using TOP with variables
SELECT TOP(@p) * FROM HumanResources.Employee;

--The rows referenced in the TOP expression used with INSERT, UPDATE, MERGE, or DELETE are not arranged in any order. TOP n returns n random rows. For example, the following INSERT statement contains the ORDER BY clause, and yet this clause does not affect the rows directly referenced by the INSERT statement.
INSERT TOP (2) INTO Table2 (ColumnB) 
    SELECT ColumnA FROM Table1 
    ORDER BY ColumnA;


SELECT TOP(10) PERCENT WITH TIES
pp.FirstName, pp.LastName, e.JobTitle, e.Gender, r.Rate
FROM Person.Person AS pp    


--A. Using TOP with variables
SELECT TOP(@p) * FROM HumanResources.Employee;

--The rows referenced in the TOP expression used with INSERT, UPDATE, MERGE, or DELETE are not arranged in any order. TOP n returns n random rows. For example, the following INSERT statement contains the ORDER BY clause, and yet this clause does not affect the rows directly referenced by the INSERT statement.
INSERT TOP (2) INTO Table2 (ColumnB) 
    SELECT ColumnA FROM Table1 
    ORDER BY ColumnA;
    
    
SELECT TOP(10) PERCENT WITH TIES
pp.FirstName, pp.LastName, e.JobTitle, e.Gender, r.Rate
FROM Person.Person AS pp     



--Find all LastNames that start with the letter A
SELECT * FROM Employee WHERE LastName LIKE 'A%'

--Find all LastNames that start with the letter B OR A
SELECT * FROM Employee WHERE LastName LIKE 'A%' OR LastName LIKE 'B%'

--LastNames ranging from A to K using a set of 11 letters
SELECT * FROM Employee WHERE LastName LIKE '[ABCDEFGHIJK]%'

--Find all LastNames starting with A or K (Mistake
SELECT * FROM Employee WHERE LastName LIKE '[AK]%'

--LastNames ranging from A to K using a range
SELECT * FROM Employee WHERE LastName LIKE '[A-K]%'

--Bad query (it won’t error but returns no records) Note: this range will not work if your LIKE was changed to an equal (=) sign.
SELECT * FROM Employee WHERE LastName = '[A-K]%'


--Finding Apostrophes in string and text
--Bad query results in an error.
--SELECT * FROM [GRANT] WHERE GrantName LIKE '%'%'

--Find GrantNames without a single quote
SELECT * FROM [GRANT] WHERE GrantName NOT LIKE '%''%'


--Querying Special Characters
--Finding literal % signs with wildcards

--Bad query pattern logic (finds all Grant records)
SELECT * FROM [GRANT] WHERE GrantName LIKE '%%%'

--Find Grants where A is the 2nd letter.
SELECT * FROM [GRANT] WHERE GrantName LIKE '_A%'

--Table-Valued Functions
SELECT * FROM GetAllProducts() -- select statemtne using Table-Valued Functions

SELECT * FROM GetCategoryProducts('Medium-stay') ---- select statemtne using Table-Valued Functions using parameter



--example uses DISTINCT to prevent the retrieval of duplicate titles.
SELECT DISTINCT JobTitle FROM HumanResources.Employee

SELECT AVG(DISTINCT ListPrice) FROM Production.Product

-- Get top rows
SELECT TOP 2 * FROM Customers;
SELECT TOP 50 PERCENT * FROM Customers;

--Get top N rows
SELECT TOP (@NoOfRows) * FROM Product

--Alias Name
SELECT CustomerName, Address + ', ' + City + ', ' + PostalCode AS Address
FROM Customers;

--Specifying multiple values as a derived table in a FROM clause
SELECT * FROM (VALUES (1, 2), (3, 4), (5, 6), (7, 8)) AS MyTable(a,b)

--Using VALUES As a Table Source
SELECT DegreeNM, DegreeCD, ModifiedDT
FROM
(VALUES
('Bachelor of Arts', 'B.A.', GETDATE()),
('Bachelor of Science', 'B.S.', GETDATE()),
('Master of Arts', 'M.A.', GETDATE()),
('Master of Science', 'M.S.', GETDATE()),
('Associate''s Degree', 'A.A.', GETDATE()))

--Ordering by two columns. 
-- This query first sorts in ascending order by the FirstName column, then sorts in descending order by the LastName column.
SELECT LastName, FirstName FROM Person.Person
WHERE LastName LIKE 'R%'
ORDER BY FirstName ASC, LastName DESC ;    

-- Load row data into the variable
SELECT @COMPLAINT = COMPLAINT,
       @DISPATCHCMTS = DISPATCHCMTS
FROM   WCSV_INCIDENT_Detail
WHERE ICRNUMBER = '111000001'

SELECT @var1 = 'Generic Name' 
SELECT @var1 = (SELECT Name  FROM Sales.Store WHERE CustomerID = 1000) 
SELECT @var1 AS 'Company Name' ;


--The following example shows two ways to use the INDEX optimizer hint. 
-- The first example shows how to force the optimizer to use a nonclustered index to retrieve rows from a table, and the second example forces a table scan by using an index of 0.
SELECT pp.FirstName, pp.LastName, e.NationalIDNumber
FROM HumanResources.Employee AS e WITH (INDEX(AK_Employee_NationalIDNumber))
JOIN Person.Person AS pp on e.BusinessEntityID = pp.BusinessEntityID
WHERE LastName = 'Johnson';

-- Force a table scan by using INDEX = 0.
SELECT pp.LastName, pp.FirstName, e.JobTitle
FROM HumanResources.Employee AS e WITH (INDEX = 0) JOIN Person.Person AS pp
ON e.BusinessEntityID = pp.BusinessEntityID
WHERE LastName = 'Johnson';

--Using UNION of two SELECT statements with ORDER BY

/* INCORRECT -- Error*/ 
SELECT ProductModelID, Name
FROM Production.ProductModel
WHERE ProductModelID NOT IN (3, 4)
ORDER BY Name
UNION
SELECT ProductModelID, Name
FROM dbo.Gloves;
GO

/* CORRECT */
SELECT ProductModelID, Name
FROM Production.ProductModel
WHERE ProductModelID NOT IN (3, 4)
UNION
SELECT ProductModelID, Name
FROM dbo.Gloves
ORDER BY Name;
GO

--Using SELECT with column headings and calculations
SELECT Name AS ProductName, 
NonDiscountSales = (OrderQty * UnitPrice),
Discounts = ((OrderQty * UnitPrice) * UnitPriceDiscount)
FROM Production.Product
GO


``` 

## SELECT Join

``` sql 

--INNER JOIN
SELECT InvoiceNumber, VendorName From Vendors INNER JOIN Invoices ON Vendors.VendorID =  Invoices.Vendors.VendorID  

-- Get all the name with or without address
SELECT Name, Age, Address, City from NameTable N LEFT JOIN ADDRESS A ON N.NameID = A.NameID

-- Get all the address with or without names
SELECT Name, Age, Address, City from NameTable N RIGHT JOIN ADDRESS A ON N.NameID = A.NameID

-- Get all the name and address with or without names
SELECT Name, Age, Address, City from NameTable N FULL JOIN ADDRESS A ON N.NameID = A.NameID

``` 

## SELECT Group

``` sql 

-- Grouping & Having

--example finds the total of each sales order in the database.
SELECT SalesOrderID, SUM(LineTotal) AS SubTotal
FROM Sales.SalesOrderDetail
GROUP BY SalesOrderID       

--example finds the average price and the sum of year-to-date sales, grouped by product ID and special offer ID.
SELECT ProductID, SpecialOfferID, AVG(UnitPrice) AS 'Average Price', 
    SUM(LineTotal) AS SubTotal
FROM Sales.SalesOrderDetail
GROUP BY ProductID, SpecialOfferID
ORDER BY ProductID;   

--example groups by an expression. You can group by an expression if the expression does not include aggregate functions.
SELECT AVG(OrderQty) AS 'Average Quantity', 
NonDiscountSales = (OrderQty * UnitPrice)
FROM Sales.SalesOrderDetail
GROUP BY (OrderQty * UnitPrice)
ORDER BY (OrderQty * UnitPrice) DESC;

-- example finds the average price of each type of product and orders the results by average price.
SELECT ProductID, AVG(UnitPrice) AS 'Average Price'
FROM Sales.SalesOrderDetail
WHERE OrderQty > 10
GROUP BY ProductID
ORDER BY AVG(UnitPrice);


--example that follows shows a HAVING clause with an aggregate function. 
-- It groups the rows in the SalesOrderDetail table by product ID and eliminates products whose average order quantities are five or less. 
SELECT ProductID 
FROM Sales.SalesOrderDetail
GROUP BY ProductID
HAVING AVG(OrderQty) > 5
ORDER BY ProductID;


SELECT ProductID, AVG(OrderQty) AS AverageQuantity, SUM(LineTotal) AS Total
FROM Sales.SalesOrderDetail
GROUP BY ProductID
HAVING SUM(LineTotal) > $1000000.00
AND AVG(OrderQty) < 3;


--If you want to make sure there are at least one thousand five hundred items involved in the calculations for each product, use HAVING COUNT(*) > 1500 to eliminate the products that return totals for fewer than 1500 items sold. 
SELECT ProductID, SUM(LineTotal) AS Total
FROM Sales.SalesOrderDetail
GROUP BY ProductID
HAVING COUNT(*) > 1500;


--This query calculates the sum of the orders, for products with prices less than $5.00, for each type of product.
SELECT ProductID, LineTotal
FROM Sales.SalesOrderDetail
WHERE UnitPrice < $5.00
ORDER BY ProductID, LineTotal
COMPUTE SUM(LineTotal) BY ProductID;
--COMPUTE SUM(LineTotal), MAX(LineTotal) BY ProductID; --The COMPUTE BY clause uses two different aggregate functions.

--The COMPUTE keyword can be used without BY to generate grand totals, grand counts, and so on.
SELECT ProductID, OrderQty, UnitPrice, LineTotal
FROM Sales.SalesOrderDetail
WHERE UnitPrice < $2.00
COMPUTE SUM(OrderQty), SUM(LineTotal);

--You can use COMPUTE BY and COMPUTE without BY in the same query. 
--The following query finds the sum of order quantities and line totals by product type, and then computes the grand total of order quantities and line totals.
SELECT ProductID, OrderQty, UnitPrice, LineTotal
FROM Sales.SalesOrderDetail
WHERE UnitPrice < $5.00
ORDER BY ProductID
COMPUTE SUM(OrderQty), SUM(LineTotal) BY ProductID
COMPUTE SUM(OrderQty), SUM(LineTotal);

--example returns only those orders whose unit price is less than $5, and then computes the line total sum by product and the grand total. All computed columns appear within the select list.
SELECT ProductID, OrderQty, SUM(LineTotal) AS Total
FROM Sales.SalesOrderDetail
WHERE UnitPrice < $5.00
GROUP BY ProductID, OrderQty
ORDER BY ProductID, OrderQty
COMPUTE SUM(SUM(LineTotal)) BY ProductID, OrderQty
COMPUTE SUM(SUM(LineTotal));


--example shows how the OPTION (GROUP) clause is used with a GROUP BY clause.
SELECT ProductID, OrderQty, SUM(LineTotal) AS Total
FROM Sales.SalesOrderDetail
WHERE UnitPrice < $5.00
GROUP BY ProductID, OrderQty
ORDER BY ProductID, OrderQty
OPTION (HASH GROUP, FAST 10);


--example uses the MERGE UNION query hint.
SELECT * FROM HumanResources.Employee AS e1
UNION
SELECT * FROM HumanResources.Employee AS e2
OPTION (MERGE UNION);



--Specifies a search condition for a group or an aggregate. HAVING can be used only with the SELECT statement. HAVING is typically used in a GROUP BY clause. When GROUP BY is not used, HAVING behaves like a WHERE clause.
SELECT SalesOrderID, SUM(LineTotal) AS SubTotal
FROM Sales.SalesOrderDetail
GROUP BY SalesOrderID
HAVING SUM(LineTotal) > 100000.00
ORDER BY SalesOrderID ;


SELECT COUNT(*) as TotalOrders, 
YEAR(OrderDate) as OrderYear,
MONTH(OrderDate) as OrderMonth
FROM Orders
GROUP BY YEAR(OrderDate), MONTH(OrderDate)
ORDER BY YEAR(OrderDate), MONTH(OrderDate)


--with case statement
SELECT
  calling_party,
  SUM(Case WHEN Event_Type=4 THEN END_TIME-START_TIME ELSE 0 END) AS total_talking_time,
  SUM(Case WHEN Event_Type=7 THEN END_TIME-START_TIME ELSE 0 END) AS total_ringing_time,
  MAX(Case WHEN Event_Type=4 THEN END_TIME-START_TIME ELSE 0 END) AS max_talking_time
FROM
  Event
WHERE
    calling_party LIKE '%(%)'
Group BY
  calling_party


--GROUP BY CUBE 
SELECT i.Shelf,
SUM(i.Quantity) Total
FROM Production.ProductInventory i
GROUP BY CUBE (i.Shelf)

-- GROUP BY ROLLUP
SELECT i.Shelf,
p.Name,
SUM(i.Quantity) Total
FROM Production.ProductInventory i
INNER JOIN Production.Product p ON
i.ProductID = p.ProductID
GROUP BY ROLLUP (i.Shelf, p.Name)

--GROUP BY GROUPING SETS
SELECT
i.Shelf,
i.LocationID,
p.Name,
SUM(i.Quantity) Total
FROM Production.ProductInventory i
INNER JOIN Production.Product p ON
i.ProductID = p.ProductID
WHERE Shelf IN ('A','C') AND
Name IN ('Chain', 'Decal', 'Head Tube')
GROUP BY GROUPING SETS
((i.Shelf), (i.Shelf, p.Name), (i.LocationID, p.Name))


--GROUP BY CUBE
SELECT
i.Shelf,
i.LocationID,
CASE
WHEN GROUPING(i.Shelf) = 0 AND
GROUPING(i.LocationID) = 1 THEN 'Shelf Total'
WHEN GROUPING(i.Shelf) = 1 AND
GROUPING(i.LocationID) = 0 THEN 'Location Total'
WHEN GROUPING(i.Shelf) = 1 AND
GROUPING(i.LocationID) = 1 THEN 'Grand Total'
ELSE 'Regular Row'
END RowType,
SUM(i.Quantity) Total
FROM Production.ProductInventory i
WHERE LocationID = 2
GROUP BY CUBE (i.Shelf,i.LocationID)

--GROUP BY ALL
SELECT OrderDate,
SUM(TotalDue) TotalDueByOrderDate
FROM Sales.SalesOrderHeader
WHERE OrderDate BETWEEN '7/1/2001' AND '7/31/2001'
GROUP BY ALL OrderDate

--Using OPTION and the GROUP hints, example shows how the OPTION (GROUP) clause is used with a GROUP BY clause.
SELECT ProductID, OrderQty, SUM(LineTotal) AS Total
FROM Sales.SalesOrderDetail
WHERE UnitPrice < $5.00
GROUP BY ProductID, OrderQty
ORDER BY ProductID, OrderQty
OPTION (HASH GROUP, FAST 10);



``` 

## SELECT SubQueries

``` sql 

SELECT
ID = (SELECT TOP 1 CUSTOMERID FROM IDTABLE ) AS ID -- Subquery
NAME
FROM Invoices
WHERE InvoiceToTAL > (SELECT AVG(InvoiceTotal) FROM Invoices)	-- Subquery in WHERE clause
ORDER BY InvoiceTotal



--Using correlated subqueries
--The following example shows queries that are semantically equivalent and illustrates the difference between using the EXISTS keyword and the IN keyword. 
-- Both are examples of a valid subquery that retrieves one instance of each product name for which the product model is a long sleeve logo jersey, and the ProductModelID numbers match between the Product and ProductModel tables.
SELECT DISTINCT Name
FROM Production.Product AS p 
WHERE EXISTS
    (SELECT *
     FROM Production.ProductModel AS pm 
     WHERE p.ProductModelID = pm.ProductModelID
           AND pm.Name LIKE 'Long-Sleeve Logo Jersey%');
-- OR
SELECT DISTINCT Name
FROM Production.Product
WHERE ProductModelID IN
    (SELECT ProductModelID 
     FROM Production.ProductModel
     WHERE Name LIKE 'Long-Sleeve Logo Jersey%');

--A correlated subquery can also be used in the HAVING clause of an outer query. 
SELECT p1.ProductModelID
FROM Production.Product AS p1
GROUP BY p1.ProductModelID
HAVING MAX(p1.ListPrice) >= ALL
    (SELECT AVG(p2.ListPrice)
     FROM Production.Product AS p2
     WHERE p1.ProductModelID = p2.ProductModelID);


--This example uses two correlated subqueries to find the names of employees who have sold a particular product.     
SELECT DISTINCT pp.LastName, pp.FirstName 
FROM Person.Person pp JOIN HumanResources.Employee e
ON e.BusinessEntityID = pp.BusinessEntityID WHERE pp.BusinessEntityID IN 
(SELECT SalesPersonID 
FROM Sales.SalesOrderHeader
WHERE SalesOrderID IN 
    (SELECT SalesOrderID 
    FROM Sales.SalesOrderDetail
    WHERE ProductID IN 
        (SELECT ProductID 
        FROM Production.Product p 
        WHERE ProductNumber = 'BK-M68B-42')));  



-- Subquery
--checking for the existence of matching rows within a correlated subquery
SELECT DISTINCT s.PurchaseOrderNumber
FROM Sales.SalesOrderHeader s
WHERE EXISTS ( SELECT SalesOrderID
FROM Sales.SalesOrderDetail
WHERE UnitPrice BETWEEN 1000 AND 2000 AND
SalesOrderID = s.SalesOrderID)

--a regular non-correlated subquery
SELECT BusinessEntityID,
SalesQuota CurrentSalesQuota
FROM Sales.SalesPerson
WHERE SalesQuota =
(SELECT MAX(SalesQuota)
FROM Sales.SalesPerson)


--Using Derived Tables
SELECT DISTINCT s.PurchaseOrderNumber
FROM Sales.SalesOrderHeader s
INNER JOIN (SELECT SalesOrderID
FROM Sales.SalesOrderDetail
WHERE UnitPrice BETWEEN 1000 AND 2000) d ON
s.SalesOrderID = d.SalesOrderID



--Using Subqueries as Lists
SELECT FirstName, LastName
FROM dbo.Contact
WHERE Region IN (Subquery that returns a list of states);

--Nested Subqueries
SELECT Name as ProductName
FROM SalesLT.Product
WHERE ProductID IN
	(SELECT ProductID
	FROM SalesLT.SalesOrderDetail
	WHERE SalesOrderID IN
		(SELECT SalesOrderID -- Find the Orders with vests
		FROM SalesLT.SalesOrderDetail
		WHERE ProductID IN
			(SELECT ProductID
			FROM SalesLT.Product
			WHERE ProductCategoryID =
				-- 1. Find the Vests category
				(Select ProductCategoryID
				FROM SalesLT.ProductCategory
				Where Name = 'Vests' ) ) ) );

--Using Subqueries as Tables
SELECT P1.Name,
a.ProductID ,
a.ProductTotal ,
a.ModifiedDate
FROM SalesLT.Product p1
JOIN (SELECT sod.ProductID,
		SUM(sod.LineTotal) AS 'ProductTotal',
		sod.ModifiedDate
	FROM SalesLT.SalesOrderDetail sod
	JOIN SalesLT.Product p
		ON sod.ProductID = p.ProductID
	JOIN SalesLT.ProductCategory pc
		ON p.ProductCategoryID = pc.ProductCategoryID
	WHERE pc.Name = 'Vests'
	GROUP BY sod.ProductID, sod.ModifiedDate
	)a
	ON p1.ProductID = a.ProductID


--All, Some, and Any
SELECT 'True' as 'AllTest'
WHERE 1 < ALL
	(SELECT a
		FROM
		(VALUES
		(2),
		(3),
		(5),
		(7),
		(9)) AS ValuesTable(a) );
--Returns True

--Be careful with the ALL condition if the subquery might return a null. A null value in
--the subquery results forces the ALL to return a false because it’s impossible to prove that
--the test is true for every value in the subquery if one of those values is unknown.
SELECT 'True' AS 'AllTest'
WHERE 1 < ALL
(SELECT a
FROM
(VALUES
(2),
(3),
(5),
(7),
(null)
) AS ValuesTable(a)
);


SELECT 'True' as 'SomeTest'
WHERE 5 = SOME
(SELECT a
FROM
(VALUES
(2),
(3),
(5),
(7),
(9)
) AS MyTable(a)
);
--Returns True


--Correlated Subqueries
SELECT p.ProductID , p.ProductCategoryID , p.Name
FROM SalesLT.Product p
WHERE ListPrice <
(SELECT
SUM(OrderQty * UnitPrice) /Sum(sod.OrderQty)
AS AveragePricePerItemInCategory
FROM SalesLT.SalesOrderDetail AS sod
INNER JOIN SalesLT.Product AS pd
ON sod.ProductID = pd.ProductID
INNER JOIN SalesLT.ProductCategory AS pc
ON pd.ProductCategoryID = pc.ProductCategoryID
WHERE pc.ProductCategoryID = p.ProductCategoryID
GROUP BY pc.Name)


``` 


## SELECT Summarize Data
• Returning a sampling of rows using TABLESAMPLE
• Using PIVOT to convert values into columns, and using an aggregation to group the data by the new columns
• Using UNPIVOT to normalize repeating column groups
• Using INTERSECT and EXCEPT operands to return distinct rows that only exist in either the left query (using EXCEPT), or only distinct rows that exist in both the left and right queries (using INTERSECT)
• Use CUBE to add summarizing total values to a result set based on columns in the GROUP BY clause.
• Use ROLLUP with GROUP BY to add hierarchical data summaries based on the ordering of columns in the GROUP BY clause.
• Use the GROUPING SETS operator to define custom aggregates in a single result set without having to use UNION ALL.

``` sql 

The SQL EXCEPT clause/operator is used to combine two SELECT statements and returns rows from the first SELECT statement that are not returned by the second SELECT statement. This means EXCEPT returns only rows, which are not available in second SELECT statement.

SELECT CustomerFirst, CustomerLast FROM Customers
EXCEPT
SELECT FirstName, LastName FROM Employee


SELECT CustomerFirst, CustomerLast FROM Customers
INTERSECT
SELECT FirstName, LastName FROM Employee


-- Get grand summery of all inventory
SELECT VendorID, COUNT(*) AS InvoiceCount, SUM(InvoiceTotal) AS InvoiceTotal
From Invoices
GROUP BY VendorID WITH ROLLUP


-- Get summery total QtyVendors for each State and finally grand total row
SELECT VendorState, VendorCity, COUNT(*) AS QtyVendors 
From Vendors
WHERE VendorState IN('IA','NJ')
GROUP BY VendorState, VendorCity WITH ROLLUP
ORDER BY VendorState, VendorCity 



SELECT VendorID, COUNT(*) AS InvoiceCount, SUM(InvoiceTotal) AS InvoiceTotal
From Invoices
GROUP BY VendorID WITH CUBE



SELECT VendorState, VendorCity, COUNT(*) AS QtyVendors 
From Vendors
WHERE VendorState IN('IA','NJ')
GROUP BY GROUPING SETS (VendorState, VendorCity )
ORDER BY VendorState, VendorCity 

--example, the INTO clause in the second SELECT statement specifies that the table named ProductResults holds the final result set of the union of the designated columns of the ProductModel and Gloves tables. 
-- Gloves table result also added in ProductResults
SELECT ProductModelID, Name
INTO dbo.ProductResults
FROM Production.ProductModel
WHERE ProductModelID NOT IN (3, 4)
UNION
SELECT ProductModelID, Name FROM dbo.Gloves;








--With Row Number using OVER   
SELECT 
ROW_NUMBER() OVER(ORDER BY SalesYTD DESC) AS 'Row Number'
s.SalesYTD
FROM Sales.SalesPerson s 


--examples show using the OVER clause with aggregate functions.
SELECT SalesOrderID, ProductID, OrderQty
    ,SUM(OrderQty) OVER(PARTITION BY SalesOrderID) AS 'Total'
    ,AVG(OrderQty) OVER(PARTITION BY SalesOrderID) AS 'Avg'
    ,COUNT(OrderQty) OVER(PARTITION BY SalesOrderID) AS 'Count'
    ,MIN(OrderQty) OVER(PARTITION BY SalesOrderID) AS 'Min'
    ,MAX(OrderQty) OVER(PARTITION BY SalesOrderID) AS 'Max'
FROM Sales.SalesOrderDetail 
WHERE SalesOrderID IN(43659,43664);


--Notice that the aggregates are calculated by SalesOrderID and the Percent by ProductID is calculated for each line of each SalesOrderID.
SELECT SalesOrderID, ProductID, OrderQty
    ,SUM(OrderQty) OVER(PARTITION BY SalesOrderID) AS 'Total'
    ,CAST(1. * OrderQty / SUM(OrderQty) OVER(PARTITION BY SalesOrderID) 
        *100 AS DECIMAL(5,2))AS 'Percent by ProductID'
FROM Sales.SalesOrderDetail 
WHERE SalesOrderID IN(43659,43664);







--Using HASH and MERGE join hints
SELECT p.Name AS ProductName, v.Name AS VendorName
FROM Production.Product AS p 
INNER MERGE JOIN Purchasing.ProductVendor AS pv 
ON p.ProductID = pv.ProductID
INNER HASH JOIN Purchasing.Vendor AS v
ON pv.BusinessEntityID = v.BusinessEntityID
ORDER BY p.Name, v.Name ;

--Using a derived table
SELECT RTRIM(p.FirstName) + ' ' + LTRIM(p.LastName) AS Name, d.City
FROM Person.Person AS p
INNER JOIN HumanResources.Employee e ON p.BusinessEntityID = e.BusinessEntityID 
INNER JOIN
   (SELECT bea.BusinessEntityID, a.City 
    FROM Person.Address AS a
    INNER JOIN Person.BusinessEntityAddress AS bea
    ON a.AddressID = bea.AddressID) AS d
ON p.BusinessEntityID = d.BusinessEntityID
ORDER BY p.LastName, p.FirstName;

--Using TABLESAMPLE to read data from a sample of rows in a table
SELECT * FROM Sales.Customer TABLESAMPLE SYSTEM (10 PERCENT) ;

-- Using PIVOT and UNPIVOT
SELECT VendorID, [250] AS Emp1, [251] AS Emp2, [256] AS Emp3, [257] AS Emp4, [260] AS Emp5
FROM 
(SELECT PurchaseOrderID, EmployeeID, VendorID
FROM Purchasing.PurchaseOrderHeader) AS p
PIVOT
(
COUNT (PurchaseOrderID)
FOR EmployeeID IN
( [250], [251], [256], [257], [260] )
) AS pvt
ORDER BY VendorID;



``` 

## Windowing and Ranking

``` sql

--Windowing
--The OVER() Clause
SELECT
ROW_NUMBER() OVER(Order By ShipDate) AS RowNumber,
PurchaseOrderID,
ShipDate
FROM Purchasing.PurchaseOrderHeader
WHERE EmployeeID = 259
ORDER BY RowNumber

--Partitioning Within the Window
SELECT
	ROW_NUMBER()
	OVER(
		PARTITION BY YEAR(ShipDate), Month(ShipDate)
		Order By ShipDate
	) AS RowNumber,
	PurchaseOrderID,
	ShipDate
FROM Purchasing.PurchaseOrderHeader
WHERE EmployeeID = 259
ORDER BY RowNumber

--Ranking Functions
``` 

## SELECT Solution

``` sql 

--the first condition tests whether each total_price is greater than the total price of every item in order number 1023. The second condition uses the MAX aggregate function to produce the same results.
total_price > ALL (SELECT total_price FROM items WHERE order_num = 1023)

total_price > (SELECT MAX(total_price) FROM items WHERE order_num = 1023)









--Finding Duplicates with SQL (3 solutions)
SELECT email,  COUNT(email) AS NumOccurrences FROM users GROUP BY email HAVING ( COUNT(email) > 1 )

SELECT T1.* FROM T1, T2 WHERE T1.C1 = T2.C1 AND T1.C2 = T2.C2 AND T1.ID <> T2.ID 

SELECT name, email COUNT(name) AS NumOccurName, COUNT(email) as NumOccurEmail FROM users GROUP BY Name, Email HAVING ( COUNT(name) > 1 ) AND ( COUNT(email) > 1)


SELECT  (SELECT COUNT(*) FROM Sales.SalesOrderDetail WHERE SalesOrderID = SOH.SalesOrderID) AS c, *
FROM    Sales.SalesOrderHeader SOH
ORDER by (SELECT COUNT(*) FROM Sales.SalesOrderDetail WHERE SalesOrderID = SOH.SalesOrderID) DESC



--How to concatenate rows? Answer is, use XML PATH.
USE AdventureWorks2008R2

SELECT      CAT.Name AS [Category],
            SUB.Name AS [Sub Category]
FROM        Production.ProductCategory CAT
INNER JOIN  Production.ProductSubcategory SUB
            ON CAT.ProductCategoryID = SUB.ProductCategoryID


The desired output here is to concatenate the subcategories in a single row as:

--achieve by using FOR XML PATH(),above query needs to be modified to concatenate the rows:
SELECT      CAT.Name AS [Category],
            STUFF((    SELECT ',' + SUB.Name AS [text()]
                        –- Add a comma (,) before each value
                        FROM Production.ProductSubcategory SUB
                        WHERE
                        SUB.ProductCategoryID = CAT.ProductCategoryID
                        FOR XML PATH('') –- Select it as XML
                        ), 1, 1, '' )
                        –- This is done to remove the first character (,)
                        –- from the result
            AS [Sub Categories]
FROM  Production.ProductCategory CAT

--FOR clause is used to specify either the BROWSE or the XML option. BROWSE and XML are unrelated options.
SELECT p.BusinessEntityID, FirstName, LastName, PhoneNumber AS Phone
FROM Person.Person AS p
Join Person.PersonPhone AS pph ON p.BusinessEntityID  = pph.BusinessEntityID
WHERE LastName LIKE 'G%'
ORDER BY LastName, FirstName 
FOR XML AUTO, TYPE, XMLSCHEMA, ELEMENTS XSINIL

--Paging
select * from(
select MP.CategoryCode, PO.PropertyObjectKey, PO.CaseNumber, PO.StorageLocationCode, PO.PropertyDate, PO.PropertyDescription, ROW_NUMBER() OVER (ORDER BY PropertyObjectKey DESC) as RowNumber
from PropertyObject PO
join MUIEntity ME on PO.MUISubjectKey = ME.MUISubjectKey
join MUIProperty MP on MP.MUIEntityKey = ME.MUIEntityKey
where MP.CategoryCode = 'P'
)AS RowConstrainedResult
where RowNumber  between 10001 and 10025


--Finding duplicate records based on multiple columns in SQL
SELECT field1 ,field2 ,field3 ,field4 ,COUNT (*)
  FROM test
 GROUP BY field1 ,field2 ,field3 ,field4
HAVING COUNT(*) > 1


``` 


## Four Ranking Function

``` sql 
--Get row number for each vendor name
SELECT ROW_NUMBER() OVER(ORDER BY VendorName) AS RowNumber, VendorName
FROM Vendors


--Get row number for each vendor state, resets for each state
SELECT ROW_NUMBER() OVER(PARTITION VendorState ORDER BY VendorName) AS RowNumber, VendorName, VendorState
FROM Vendors


SELECT 
RANK() OVER (ORDER BY InvoiceTotal) AS Rank,
DENSE_RANK() OVER (ORDER BY InvoiceTotal) AS DenseRank,
InvoiceTotal, OnvoceNumber
From Invoices


SELECT Terms
NTILE(2) OVER (ORDER BY TermsID) AS Tile2,
NTILE(3) OVER (ORDER BY TermsID) AS Tile3,
NTILE(4) OVER (ORDER BY TermsID) AS Tile42
FROM Terms

```

## Analytic Functions

``` sql 
FIRST_VALUE LAST_VALUE
LEAD LET
PERCENT_RANK CUME_DIST
PERCENTILE_CONT PERCENTILE_DISC
```

## Insert Statements

``` sql 
--A. Inserting a single row of data
-- Column order should match
INSERT INTO Production.UnitMeasure VALUES (N'FT', N'Feet', '20080414'); 

--B. Inserting multiple rows of data
--example uses the table value constructor to insert three rows into the Production.UnitMeasure table in a single INSERT statement. 
INSERT INTO Production.UnitMeasure
VALUES (N'FT2', N'Square Feet ', '20080923'), (N'Y', N'Yards', '20080923'), (N'Y3', N'Cubic Yards', '20080923');



-- This statement fails because the third values list contains multiple columns in the subquery.
INSERT INTO dbo.MyProducts (Name, ListPrice)
VALUES ('Helmet', 25.50),
       ('Wheel', 30.00),
       (SELECT Name, ListPrice FROM Production.Product WHERE ProductID = 720);
       
--Works
INSERT INTO dbo.MyProducts (Name, ListPrice)
VALUES ('Helmet', 25.50),
       ('Wheel', 30.00),
       ((SELECT Name FROM Production.Product WHERE ProductID = 720),
        (SELECT ListPrice FROM Production.Product WHERE ProductID = 720));       



--C. Inserting data that is not in the same order as the table columns
INSERT INTO Production.UnitMeasure (Name, UnitMeasureCode, ModifiedDate)
VALUES (N'Square Yards', N'Y2', GETDATE());

--A. Inserting data into a table with columns that have default values
CREATE TABLE dbo.T1 
(
    column_1 AS 'Computed column ' + column_2, 
    column_2 varchar(30)  CONSTRAINT default_name DEFAULT ('my column default'),
    column_3 rowversion,
    column_4 varchar(40) NULL
);
GO
INSERT INTO dbo.T1 (column_4) VALUES ('Explicit value');
INSERT INTO dbo.T1 (column_2, column_4) VALUES ('Explicit value', 'Explicit value');
INSERT INTO dbo.T1 (column_2) VALUES ('Explicit value');
INSERT INTO T1 DEFAULT VALUES; 
GO

--B. Inserting data into a table that has an identity column
--INSERT statements allow identity values to be generated for the new rows.
INSERT T1 (column_2) VALUES ('Row #2');

--INSERT statement overrides the IDENTITY property for the column with the SET IDENTITY_INSERT statement and 
--inserts an explicit value into the identity column.
SET IDENTITY_INSERT T1 ON;
GO
INSERT INTO T1 (column_1,column_2)  VALUES (-99, 'Explicit identity value');


--example uses the NEWID() function to obtain a GUID for column_2. Unlike for identity columns, the Database Engine does not automatically generate values for columns with the uniqueidentifier data type, as shown by the second INSERT statement.
INSERT INTO dbo.T1 (column_2) VALUES (NEWID());
INSERT INTO T1 DEFAULT VALUES; 
GO


--D. Inserting data into user-defined type columns
INSERT INTO dbo.Points (PointValue) VALUES (CONVERT(Point, '3,4'));


--INSERT...EXECUTE procedure example
INSERT INTO dbo.EmployeeSales 
EXECUTE dbo.uspGetEmployeeSales ‘PARAM’;
GO

--INSERT...SELECT example
INSERT INTO dbo.EmployeeSales
    SELECT 'SELECT', sp.BusinessEntityID, c.LastName, sp.SalesYTD 
    FROM Sales.SalesPerson AS
    
    
--INSERT...EXECUTE('string') example
INSERT INTO dbo.EmployeeSales 
EXECUTE 
('
SELECT ''EXEC STRING'', sp.BusinessEntityID, c.LastName, 
    sp.SalesYTD 
    FROM Sales.SalesPerson AS sp 
    INNER JOIN Person.Person AS c
        ON sp.BusinessEntityID = c.BusinessEntityID
    WHERE sp.BusinessEntityID LIKE ''2%''
    ORDER BY sp.BusinessEntityID, c.LastName
');
GO

--B. Using WITH common table expression to define the data inserted\
WITH EmployeeTemp (EmpID, LastName, FirstName)
AS (SELECT 
       e.BusinessEntityID, c.LastName, c.FirstName
    FROM HumanResources.Employee e
        INNER JOIN Person.Person as c
        ON e.BusinessEntityID = c.BusinessEntityID
    )
INSERT INTO HumanResources.NewEmployee 
    SELECT EmpID, LastName, FirstName
    FROM EmployeeTemp;
    
    
-- Insert 10 random rows into the table NewEmployee.
INSERT TOP (10) INTO HumanResources.NewEmployee 
    SELECT
       e.BusinessEntityID, e.CurrentFlag
    FROM HumanResources.Employee e
GO


--A. Inserting data by specifying a view
--example specifies a view name as the target object; however, the new row is inserted in the underlying base table. The order of the values in the INSERT statement must match the column order of the view

INSERT INTO V1 -- V1 is a view
    VALUES ('Row 1',1);
    
    
-- Insert values into the table variable.
INSERT INTO @MyTableVar (LocationID, CostRate, ModifiedDate)
    SELECT LocationID, CostRate, GETDATE() FROM Production.Location
    WHERE CostRate > 0;    
    
-- Specify the remote data source in the FROM clause using a four-part name 
-- in the form linked_server.catalog.schema.object.    
INSERT INTO MyLinkServer.AdventureWorks2008R2.HumanResources.Department (Name, GroupName)
VALUES (N'Public Relations', N'Executive General and Administration');

-- Use the OPENQUERY function to access the remote data source.
INSERT OPENQUERY (MyLinkServer, 'SELECT Name, GroupName FROM AdventureWorks2008R2.HumanResources.Department')
VALUES ('Environmental Impact', 'Engineering')

-- Use the OPENDATASOURCE function to specify the remote data source.
-- Specify a valid server name for Data Source using the format server_name or server_name\instance_name.
INSERT INTO OPENDATASOURCE('SQLNCLI',
    'Data Source= <server_name>; Integrated Security=SSPI')
    .AdventureWorks2008R2.HumanResources.Department (Name, GroupName)
    VALUES (N'Standards and Methods', 'Quality Assurance');
    
    
--A. Inserting data into a heap with minimal logging

-- Temporarily set the recovery model to BULK_LOGGED.
ALTER DATABASE AdventureWorks2008R2
SET RECOVERY BULK_LOGGED;
GO
-- Transfer data from Sales.SalesOrderDetail to Sales.SalesHistory
INSERT INTO Sales.SalesHistory WITH (TABLOCK)
    (SalesOrderID, rowguid, ModifiedDate)
SELECT * FROM Sales.SalesOrderDetail;
GO
-- Reset the recovery model.
ALTER DATABASE AdventureWorks2008R2
SET RECOVERY FULL;
GO

--B. Using the OPENROWSET function with BULK to bulk import data into a table
-- Use the OPENROWSET function to specify the data source and specifies the IGNORE_TRIGGERS table hint.
INSERT INTO HumanResources.Department WITH (IGNORE_TRIGGERS) (Name, GroupName)
SELECT b.Name, b.GroupName 
FROM OPENROWSET (
    BULK 'C:\SQLFiles\DepartmentData.txt',
    FORMATFILE = 'C:\SQLFiles\BulkloadFormatFile.xml',
    ROWS_PER_BATCH = 15000)AS b ;
GO

--A. Using the TABLOCK hint to specify a locking method
INSERT INTO Production.Location WITH (XLOCK)
(Name, CostRate, Availability)
VALUES ( N'Final Inventory', 15.00, 80.00);

--A Using OUTPUT with an INSERT statement
INSERT Production.ScrapReason
    OUTPUT INSERTED.ScrapReasonID, INSERTED.Name, INSERTED.ModifiedDate
        INTO @MyTableVar
VALUES (N'Operator error', GETDATE());

--Anotehr OUTPUT with an INSERT statement
INSERT INTO dbo.EmployeeSales (LastName, FirstName, CurrentSales)
  OUTPUT INSERTED.LastName, 
         INSERTED.FirstName, 
         INSERTED.CurrentSales
  INTO @MyTableVar
    SELECT c.LastName, c.FirstName, sp.SalesYTD
    FROM Sales.SalesPerson AS sp
    INNER JOIN Person.Person AS c
        ON sp.BusinessEntityID = c.BusinessEntityID
    WHERE sp.BusinessEntityID LIKE '2%'
    ORDER BY c.LastName, c.FirstName;


--C. Inserting data returned from an OUTPUT clause
--example captures data returned from the OUTPUT clause of a MERGE statement, and inserts that data into another table. The MERGE statement updates the Quantity column of the ProductInventory table daily, based on orders that are processed in the SalesOrderDetail table. It also deletes rows for products whose inventories drop to 0. The example captures the rows that are deleted and inserts them into another table, ZeroInventory, which tracks products with no inventory.
INSERT INTO Production.ZeroInventory (DeletedProductID, RemovedOnDate)
SELECT ProductID, GETDATE()
FROM
(   MERGE Production.ProductInventory AS pi
    USING (SELECT ProductID, SUM(OrderQty) FROM Sales.SalesOrderDetail AS sod
           JOIN Sales.SalesOrderHeader AS soh
           ON sod.SalesOrderID = soh.SalesOrderID
           AND soh.OrderDate = '20070401'
           GROUP BY ProductID) AS src (ProductID, OrderQty)
    ON (pi.ProductID = src.ProductID)
    WHEN MATCHED AND pi.Quantity - src.OrderQty <= 0
        THEN DELETE
    WHEN MATCHED
        THEN UPDATE SET pi.Quantity = pi.Quantity - src.OrderQty
    OUTPUT $action, deleted.ProductID) AS Changes (Action, ProductID)
WHERE Action = 'DELETE';


-- Create the table to accept the results
CREATE TABLE #tracestatus (TraceFlag INT, Status INT)

-- Execute the command, putting the results in the table
INSERT INTO #tracestatus  EXEC ('DBCC TRACESTATUS (-1) WITH NO_INFOMSGS')



--The row constructor looks exactly like the double INSERT INTO except that you replace subsequent INSERT INTO statements with commas 
--The second advantage is that SQL Server uses only one lock instead of two when using the row constructors feature.
--SQL Server confirms a single transaction of two rows as seen in the “2 row(s) affected” message instead of two “1 row(s) affected”
-- Inserts two rows
INSERT INTO Movie VALUES (4,'Dare or Die',110,'R'), (5,'EeeeGhads',88,'G')


``` 




## Update Statements

``` sql 
--A simple update
UPDATE suppliers SET name = 'HP' WHERE name = 'IBM';


--Conditional Update
UPDATE Staging_INBOK6 
SET 
Booking_AuthorityInvolvedKey2 = p.personnelkey,
Booking_AuthorityInvolved_FirstName2 = p.firstname,
Booking_AuthorityInvolved_LastName2 =  p.lastname
FROM Staging_INBOK6 b LEFT OUTER JOIN personnel p
ON p.personnelid = b.B6_OFF2 


--A more complex update uses another table as the source of the data. 
--This makes the UPDATE statement look like a combination of the UPDATE statement and the SELECT statement.
UPDATE TableName
SET Column2 = AnotherTable.Column3
FROM AnotherTable
WHERE TableName.Column1 = TableName.Column1


--We can add joins into this as well, so that we can update more than one column from different tables at the same time.
UPDATE TableName
SET Column2 = AnotherTable.Column3,
Column3 = ThirdTable.Column2
FROM AnotherTable JOIN ThirdTable ON AnotherTable.Column5 = ThirdTable.Column4
WHERE TableName.Column1 = TableName.Column1

--Updating Large Value Data Type Columns
UPDATE RecipeChapter
SET Chapter .WRITE('daily', 181, 10)
WHERE ChapterID = 1

--Inserting or Updating an Image File Using OPENROWSET and BULK
INSERT dbo.StockBmps (StockBmpID, bmp)
SELECT 1, BulkColumn
FROM OPENROWSET(BULK 'C:\Apress\StockPhotoOne.bmp', SINGLE_BLOB) AS x

NOTE: Use caution when specifying the FROM clause to provide the criteria for the update operation. The results of an UPDATE statement are undefined if the statement includes a FROM clause that is not specified in such a way that only one value is available for each column occurrence that is updated, that is, if the UPDATE statement is not deterministic. This can cause unexpected results. 


UPDATE suppliers	
SET city =	( SELECT customers.city FROM customers 
									WHERE customers.customer_name = suppliers.supplier_name)
WHERE EXISTS
  ( SELECT customers.city ROM customers
    WHERE customers.customer_name = suppliers.supplier_name);


-- Update using CASE
UPDATE titles
SET price = CASE
				WHEN (price < 5.0 AND ytd_sales > 999.99)
                           THEN price * 1.25
				WHEN (price > 4.99 AND ytd_sales > 999.99)
                           THEN price * 1.2
				ELSE price
			END

-- Update with OUTPUT STATEMENT
DECLARE @MyTableVar table ( SummaryBefore nvarchar(max), SummaryAfter nvarchar(max));

UPDATE Production.Document
SET DocumentSummary = 'features'
OUTPUT deleted.DocumentSummary, inserted.DocumentSummary  INTO @MyTableVar
WHERE Title = N'Front Reflector Bracket Installation';

--Using OUTPUT INTO to return an expression
UPDATE TOP (10) HumanResources.Employee
SET VacationHours = VacationHours * 1.25,
    ModifiedDate = GETDATE()
OUTPUT inserted.BusinessEntityID,
       deleted.VacationHours,
       inserted.VacationHours,
       inserted.VacationHours - deleted.VacationHours,
       inserted.ModifiedDate
INTO @MyTableVar;


-- SQL UPDATE CTE - UPDATE underlying table through CTE
WITH CTE 
     AS (SELECT Price = ListPrice 
         FROM   Product 
         WHERE  ListPrice > 1000.0) 
UPDATE CTE 
SET    Price = Price * 1.05 
GO


-- Update with JOIN 
UPDATE sp
SET sp.SalesYTD = sp.SalesYTD + sod.SubTotal
FROM SalesPerson sp
JOIN SalesOrderHeader sod
      ON sp.SalesPersonID = sod.SalesPersonID
      AND sod.OrderDate = (SELECT MAX(OrderDate)
                           FROM SalesOrderHeader
                           WHERE SalesPersonID = sp.SalesPersonID);
                           

-- SQL UPDATE applying MERGE                           
MERGE INTO tempdb.dbo.Product AS Target
USING (SELECT ProductID, ListPrice
       FROM tempdb.dbo.Product
       WHERE Color is not null AND ListPrice > 0.0)
       AS Source (ProductID, ListPrice)
ON Target.ProductID = Source.ProductID
WHEN MATCHED THEN
    UPDATE SET ListPrice= Source.ListPrice * 1.1;                        
    
    
-- UPDATE with an INNER JOIN to SELECT - GROUP BY subquery (derived table DG)    
UPDATE DE
SET DE.NoOfEmployees =DG.DeptEmployees,
    DE.ModifiedDate = CURRENT_TIMESTAMP
FROM dbo.Department DE
JOIN (SELECT D.DepartmentID, COUNT(*) AS DeptEmployees
      FROM AdventureWorks.HumanResources.EmployeeDepartmentHistory EDH
      JOIN dbo.Department D
            ON d.DepartmentID = EDH.DepartmentID
          and EDH.EndDate is null
      JOIN AdventureWorks.HumanResources.Employee E
            ON EDH.EmployeeID = E.EmployeeID
      GROUP BY D.DepartmentID ) DG
ON DE.DepartmentID = DG.DepartmentID       


--Limiting the Rows that Are Updated
UPDATE TOP (10) HumanResources.Employee
SET VacationHours = VacationHours * 1.25 ;

--The following example uses the WHERE CURRENT OF clause to update only the row on which the cursor is positioned. 
--When a cursor is based on a join, only the table_name specified in the UPDATE statement is modified. 
--Other tables participating in the cursor are not affected.
DECLARE complex_cursor CURSOR FOR
    SELECT a.BusinessEntityID
    FROM HumanResources.EmployeePayHistory AS a
    WHERE RateChangeDate <> 
         (SELECT MAX(RateChangeDate)
          FROM HumanResources.EmployeePayHistory AS b
          WHERE a.BusinessEntityID = b.BusinessEntityID) ;
OPEN complex_cursor;
FETCH FROM complex_cursor;
UPDATE HumanResources.EmployeePayHistory
SET PayFrequency = 2 
WHERE CURRENT OF complex_cursor;
CLOSE complex_cursor;
DEALLOCATE complex_cursor;
GO


--uses a subquery in the SET clause to determine the value that is used to update the column. 
--The subquery must return only a scalar value (that is, a single value per row).
UPDATE Sales.SalesPerson
SET SalesYTD = SalesYTD + 
    (SELECT SUM(so.SubTotal) 
     FROM Sales.SalesOrderHeader AS so
     WHERE so.OrderDate = (SELECT MAX(OrderDate)
                           FROM Sales.SalesOrderHeader AS so2
                           WHERE so2.SalesPersonID = so.SalesPersonID)
     AND Sales.SalesPerson.BusinessEntityID = so.SalesPersonID
     GROUP BY so.SalesPersonID);
GO


-- sets the CostRate column to its default value (0.00) 
UPDATE Production.Location
SET CostRate = DEFAULT WHERE CostRate > 20.00;


--Target Objects Other Than Tables: Specifying a view as the target object
-- example updates rows in a table by specifying a view as the target object. 
--The view definition references multiple tables, however, the UPDATE statement succeeds because it references columns from only 
--one of the underlying tables. 
--The UPDATE statement would fail if columns from both tables were specified. 
UPDATE Person.vStateProvinceCountryRegion
SET CountryRegionName = 'United States of America'
WHERE CountryRegionName = 'United States';


--Target Objects Other Than Tables: Specifying a table alias as the target object
UPDATE sr
SET sr.Name += ' - tool malfunction'
FROM Production.ScrapReason AS sr
JOIN Production.WorkOrder AS wo 
     ON sr.ScrapReasonID = wo.ScrapReasonID
     AND wo.ScrappedQty > 300;


--Target Objects Other Than Tables: Specifying a table variable as the target object
UPDATE @MyTableVar
SET NewVacationHours = e.VacationHours + 20,
    ModifiedDate = GETDATE()
FROM HumanResources.Employee AS e 
WHERE e.BusinessEntityID = EmpID;


--Updating data in a remote table by using a linked server
UPDATE MyLinkServer.AdventureWorks.HumanResources.Department
SET GroupName = N'Public Relations'
WHERE DepartmentID = 4;

--Updating data in a remote table by using the OPENQUERY function
UPDATE OPENQUERY (MyLinkServer, 'SELECT GroupName FROM HumanResources.Department WHERE DepartmentID = 4') 
SET GroupName = 'Sales and Marketing';

--Updating data in a remote table by using the OPENDATASOURCE function
UPDATE OPENDATASOURCE('SQLNCLI', 'Data Source=London\Payroll;Integrated Security=SSPI')
    .AdventureWorks2008R2.HumanResources.Employee
SET GroupName = 'Sales and Marketing';



--A. Using UPDATE with .WRITE to modify data in an nvarchar(max) column
UPDATE Production.Document
SET DocumentSummary .WRITE (N'features',28,10)
OUTPUT deleted.DocumentSummary, 
       inserted.DocumentSummary 
    INTO @MyTableVar
WHERE Title = N'Front Reflector Bracket Installation';



--Using UPDATE with OPENROWSET to modify a varbinary(max) column
UPDATE Production.ProductPhoto
SET ThumbNailPhoto = (
    SELECT *
    FROM OPENROWSET(BULK 'c:\Tires.jpg', SINGLE_BLOB) AS x )
WHERE ProductPhotoID = 1;


--You can update a UDT by invoking a method,
UPDATE dbo.Cities
SET Location.SetXY(23.5, 23.5)
WHERE Name = 'Anchorage';

--Modifying the value of a property or data member
--update UDT by modifying the value of a registered property or public data member of the user-defined type. 
--expression supplying the value must be implicitly convertible to the type of the property.
UPDATE dbo.Cities
SET Location.X = 23.5
WHERE Name = 'Anchorage';


--Specifying a table hint
--example specifies the table hint TABLOCK. This hint specifies that a shared lock is taken on the table Production.
--Product and held until the end of the UPDATE statement.
UPDATE Production.Product
WITH (TABLOCK)
SET ListPrice = ListPrice * 1.10
WHERE ProductNumber LIKE 'BK-%';


Updating Multiple Records from another Table
A common query to write is where a table is to be updated based on information in another table.  In T-SQL this is very easy to do.  Many beginners will actually try to do more work by writing code outside of the database or writing cursors to loop through a query set and run a bunch of UPDATE statements.  This creates a lot of overhead and wastes time writing the statements.

Let's say you had a customer table that you added a column to called LastOrderDate.  This is a datetime column and indicates the last time a customer has placed an order.  Once created there is a need to backfill the data.  To do this you would simply write an UPDATE query with a FROM clause containing the Orders table.


UPDATE dbo.Customers
SET LastOrderDate = dbo.Orders.OrderDate
FROM dbo.Orders
WHERE dbo.Orders.CustKey = dbo.Customers.CustKey


Of course, multiple orders can lead to interesting update results where you might not get the last order date.  Using a view as the join, we can pull the last order date.

UPDATE dbo.Customers
SET LastOrderDate = dbo.Orders.OrderDate
FROM (SELECT Max(OrderDate) AS OrderDate, CustKey 
        FROM dbo.Orders 
        GROUP BY CustKey) O
WHERE O.CustKey = dbo.Customers.CustKey


This makes more sense because hopefully our customer's are ordering more than once. 



``` 


## Delete Statements

``` sql 

DELETE FROM Sales.SalesPersonQuotaHistory;

DELETE FROM Production.ProductCostHistory
WHERE StandardCost > 1000.00;


--Using DELETE on the current row of a cursor
DECLARE complex_cursor CURSOR FOR
    SELECT a.BusinessEntityID
    FROM HumanResources.EmployeePayHistory AS a
    WHERE RateChangeDate <> 
         (SELECT MAX(RateChangeDate)
          FROM HumanResources.EmployeePayHistory AS b
          WHERE a.BusinessEntityID = b.BusinessEntityID) ;
OPEN complex_cursor;
FETCH FROM complex_cursor;
DELETE FROM HumanResources.EmployeePayHistory
WHERE CURRENT OF complex_cursor;
CLOSE complex_cursor;
DEALLOCATE complex_cursor;
GO

-- Using DELETE based on a subquery and using the Transact-SQL extension
DELETE FROM Sales.SalesPersonQuotaHistory 
WHERE BusinessEntityID IN 
    (SELECT BusinessEntityID 
     FROM Sales.SalesPerson 
     WHERE SalesYTD > 2500000.00);
     
     
     
DELETE FROM Sales.SalesPersonQuotaHistory 
FROM Sales.SalesPersonQuotaHistory AS spqh
INNER JOIN Sales.SalesPerson AS sp
ON spqh.BusinessEntityID = sp.BusinessEntityID
WHERE sp.SalesYTD > 2500000.00;

--E. Using DELETE with the TOP clause
DELETE TOP (2.5) PERCENT 
FROM Production.ProductInventory;

--F. Using DELETE with the OUTPUT clause
DELETE Sales.ShoppingCartItem
OUTPUT DELETED.* 
WHERE ShoppingCartID = 20621;

--G. Using OUTPUT with from_table_name in a DELETE statement
DELETE Production.ProductProductPhoto
OUTPUT DELETED.ProductID,
       p.Name,
       p.ProductModelID,
       DELETED.ProductPhotoID
    INTO @MyTableVar
FROM Production.ProductProductPhoto AS ph
JOIN Production.Product as p 
    ON ph.ProductID = p.ProductID 
    WHERE p.ProductModelID BETWEEN 120 and 130;



DELETE Top TSQL Statement

DELETE TOP (1) 
FROM Sales.Customer
WHERE CustomerID = 1

This would delete one of the duplicate rows for Customer number 1

Suppose somehow the whole customer table got duplicated.  I duplicated the Sales.Customer table into a tmpCustomer table.

SELECT Top 1 CustomerID, COUNT(CustomerID) AS Cnt
FROM tmpCustomer 
GROUP BY CustomerID
HAVING COUNT(CustomerID) > 1

WHILE @@RowCount > 0
BEGIN
    DELETE Top (1)
    FROM tmpCustomer
    WHERE CustomerID = (SELECT Top (1) CustomerID
                        FROM tmpCustomer 
                        GROUP BY CustomerID
                        HAVING COUNT(CustomerID) > 1)

END 


While this worked just fine, it ran about 4 minutes for 38K rows.  Let's try the dreaded CURSOR.   Notice I can stick a variable in where the TOP () statement is.  I subtracted -1 because we don't want to delete every row.

DECLARE @cnt int, @custID as int

DECLARE dupCursor CURSOR FAST_FORWARD
FOR SELECT CustomerID, COUNT(CustomerID) AS Cnt
    FROM tmpCustomer 
    GROUP BY CustomerID
    HAVING COUNT(CustomerID) > 1

OPEN dupCursor 

FETCH NEXT FROM dupCursor 
INTO @custID, @cnt

WHILE @@FETCH_STATUS = 0
BEGIN
    DELETE Top (@cnt-1)
    FROM tmpCustomer
    WHERE CustomerID = @custID
    
    FETCH NEXT FROM dupCursor 
    INTO @custID, @cnt
END

CLOSE dupCursor
DEALLOCATE dupCursor

This ran much better at 18 seconds.



``` 










## Output Statements

``` sql 


--Returning Data from an Insert
INSERT INTO PersonList
OUTPUT Inserted.*
VALUES(77777, 'Jane', 'Doe');

--Returning Data from an Update
UPDATE PersonList
SET FirstName = 'Jane', LastName = 'Doe'
OUTPUT Deleted.FirstName OldFirstName,Deleted.LastName OldLastName,
Inserted.FirstName NewFirstName, Inserted.LastName NewLastName
WHERE BusinessEntityID = 77777

--Returning Data from a Delete
DELETE FROM PersonList
OUTPUT DELETED.*
WHERE BusinessEntityID = 77777

--Returning Data from a Merge
MERGE FlightPassengers F
USING CheckIn C
ON C.LastName = F.LastName
AND C.FirstName = F.FirstName
AND C.FlightCode = F.FlightCode
AND C.FlightDate = F.FlightDate
WHEN MATCHED
THEN UPDATE
SET F.Seat = C.Seat
WHEN NOT MATCHED BY TARGET
THEN INSERT (FirstName, LastName, FlightCode, FlightDate, Seat)
VALUES (FirstName, LastName, FlightCode, FlightDate, Seat)
WHEN NOT MATCHED BY SOURCE
THEN DELETE
OUTPUT
deleted.FlightID, deleted.LastName, Deleted.Seat,
$action,
inserted.FlightID, inserted.LastName, inserted.Seat ;


--Returning Data into a Table
DECLARE @DeletedPerson TABLE (
BusinessEntityID INT NOT NULL PRIMARY KEY,
LastName VARCHAR(50) NOT NULL,
FirstName VARCHAR(50) NOT NULL
);
DELETE dbo.PersonList
OUTPUT Deleted.BusinessEntityID, Deleted.LastName,
Deleted.FirstName
INTO @DeletedPerson
WHERE BusinessEntityID = 2;

SELECT BusinessEntityID, LastName, FirstName FROM @DeletePerson;



--D. Using OUTPUT INTO to return an expression
UPDATE TOP (10) HumanResources.Employee
SET VacationHours = VacationHours * 1.25,
    ModifiedDate = GETDATE()
OUTPUT inserted.BusinessEntityID,
       deleted.VacationHours,
       inserted.VacationHours,
       inserted.VacationHours - deleted.VacationHours,
       inserted.ModifiedDate
INTO @MyTableVar;

--E. Using OUTPUT INTO with from_table_name in an UPDATE statement
UPDATE Production.WorkOrder
SET ScrapReasonID = 4
OUTPUT deleted.ScrapReasonID,
       inserted.ScrapReasonID, 
       inserted.WorkOrderID,
       inserted.ProductID,
       p.Name
    INTO @MyTestVar
    
--J. Using OUTPUT and OUTPUT INTO in a single statement    
DELETE Production.ProductProductPhoto
OUTPUT DELETED.ProductID,
       p.Name,
       p.ProductModelID,
       DELETED.ProductPhotoID
    INTO @MyTableVar
OUTPUT DELETED.ProductID, DELETED.ProductPhotoID, GETDATE() AS DeletedDate 
FROM Production.ProductProductPhoto AS ph
JOIN Production.Product as p 
    ON ph.ProductID = p.ProductID 
WHERE p.ProductID BETWEEN 800 and 810;    


--J. Using OUTPUT and OUTPUT INTO in a single statement
INSERT INTO Production.ZeroInventory (DeletedProductID, RemovedOnDate)
SELECT ProductID, GETDATE()
FROM
(   MERGE Production.ProductInventory AS pi
    USING (SELECT ProductID, SUM(OrderQty) FROM Sales.SalesOrderDetail AS sod
           JOIN Sales.SalesOrderHeader AS soh
           ON sod.SalesOrderID = soh.SalesOrderID
           AND soh.OrderDate = '20070401'
           GROUP BY ProductID) AS src (ProductID, OrderQty)
    ON (pi.ProductID = src.ProductID)
    WHEN MATCHED AND pi.Quantity - src.OrderQty <= 0
        THEN DELETE
    WHEN MATCHED
        THEN UPDATE SET pi.Quantity = pi.Quantity - src.OrderQty
    OUTPUT $action, deleted.ProductID) AS Changes (Action, ProductID)
WHERE Action = 'DELETE';
IF @@ROWCOUNT = 0
PRINT 'Warning: No rows were inserted';
GO


--DECLARE @SummaryOfChanges TABLE(Change VARCHAR(20));

MERGE INTO Sales.SalesReason AS Target
USING (VALUES ('Recommendation','Other'), ('Review', 'Marketing'), ('Internet', 'Promotion'))
       AS Source (NewName, NewReasonType)
ON Target.Name = Source.NewName
WHEN MATCHED THEN
	UPDATE SET ReasonType = Source.NewReasonType
WHEN NOT MATCHED BY TARGET THEN
	INSERT (Name, ReasonType) VALUES (NewName, NewReasonType)
OUTPUT $action INTO @SummaryOfChanges;

-- Query the results of the table variable.
SELECT Change, COUNT(*) AS CountPerChange
FROM @SummaryOfChanges
GROUP BY Change;
DECLARE @SummaryOfChanges TABLE(Change VARCHAR(20));

MERGE INTO Sales.SalesReason AS Target
USING (VALUES ('Recommendation','Other'), ('Review', 'Marketing'), ('Internet', 'Promotion'))
       AS Source (NewName, NewReasonType)
ON Target.Name = Source.NewName
WHEN MATCHED THEN
	UPDATE SET ReasonType = Source.NewReasonType
WHEN NOT MATCHED BY TARGET THEN
	INSERT (Name, ReasonType) VALUES (NewName, NewReasonType)
OUTPUT $action INTO @SummaryOfChanges;

-- Query the results of the table variable.
SELECT Change, COUNT(*) AS CountPerChange
FROM @SummaryOfChanges
GROUP BY Change;


``` 



## SET Statements

``` sql 
SET @myvar = 'This is a test';
SET @NewBalance  =  @NewBalance  *  10;
SET @NewBalance *= 10;

--E. Defining a cursor by using SET
SET @CursorVar = CURSOR SCROLL DYNAMIC
OPEN @CursorVar;

--F. Assigning a value from a query
SET @rows = (SELECT COUNT(*) FROM Sales.Customer);

--G. Assigning a value to a user-defined type variable by modifying a property of the type
DECLARE @p Point;
SET @p.X = @p.X + 1.1;

--H. Assigning a value to a user-defined type variable by invoking a method of the type
DECLARE @p Point;
SET @p=point.SetXY(23.5, 23.5);



------------------------------------------------------
-- Date and time statements
------------------------------------------------------

-- SET DATEFIRST to U.S. English default value of 7.
SET DATEFIRST 7;

-- Set date format to day/month/year.
SET DATEFORMAT dmy;


------------------------------------------------------
-- Locking statements
------------------------------------------------------

SET DEADLOCK_PRIORITY LOW;
SET DEADLOCK_PRIORITY NORMAL;

--Set the lock timeout to 1800 seconds
SET LOCK_TIMEOUT 1800;

--Set the lock timeout to wait forever for a lock to be released.
SET LOCK_TIMEOUT -1;


------------------------------------------------------
-- Miscellaneous statements
------------------------------------------------------

SET CURSOR_CLOSE_ON_COMMIT { ON | OFF }

SET CONCAT_NULL_YIELDS_NULL { ON | OFF } 

-- SET IDENTITY_INSERT to ON.
SET IDENTITY_INSERT dbo.Tool ON;

SET LANGUAGE us_english;
SET LANGUAGE Italian;

SET QUOTED_IDENTIFIER { ON | OFF }

------------------------------------------------------
-- Query Execution Statements
------------------------------------------------------


SET FMTONLY { ON | OFF } 

SET NOCOUNT { ON | OFF } 

SET NOEXEC { ON | OFF }

SET NUMERIC_ROUNDABORT { ON | OFF } 

SET PARSEONLY { ON | OFF }

SET ROWCOUNT 4;


SET TEXTSIZE number ; 




------------------------------------------------------
-- ISO Settings statements
------------------------------------------------------


SET ANSI_DEFAULTS { ON | OFF }
SET ANSI_NULL_DFLT_OFF { ON | OFF }
SET ANSI_NULL_DFLT_ON {ON | OFF}
SET ANSI_NULLS { ON | OFF }
SET ANSI_WARNINGS { ON | OFF }
SET ANSI_PADDING { ON | OFF }


------------------------------------------------------
-- Statistics statements
------------------------------------------------------

SET FORCEPLAN { ON | OFF }
SET SHOWPLAN_ALL { ON | OFF }
SET SHOWPLAN_TEXT { ON | OFF }
SET SHOWPLAN_XML { ON | OFF }
SET STATISTICS IO { ON | OFF }
SET STATISTICS XML { ON | OFF }
SET STATISTICS TIME { ON | OFF }
SET STATISTICS PROFILE { ON | OFF }

------------------------------------------------------
-- Transactions statements
------------------------------------------------------
SET IMPLICIT_TRANSACTIONS { ON | OFF }
SET REMOTE_PROC_TRANSACTIONS { ON | OFF } 



SET TRANSACTION ISOLATION LEVEL READ UNCOMMITTED
SET TRANSACTION ISOLATION LEVEL READ COMMITTED
SET TRANSACTION ISOLATION LEVEL REPEATABLE READ
SET TRANSACTION ISOLATION LEVEL SNAPSHOT
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE

SET XACT_ABORT { ON | OFF }





``` 





## Transcation Statements

``` sql 
--example shows how to name a transaction.
DECLARE @TranName VARCHAR(20);
SELECT @TranName = 'MyTransaction';

BEGIN TRANSACTION @TranName;
USE AdventureWorks2008R2;
DELETE FROM AdventureWorks2008R2.HumanResources.JobCandidate
    WHERE JobCandidateID = 13;

COMMIT TRANSACTION @TranName;


--The following example shows how to mark a transaction. The transaction CandidateDelete is marked.
BEGIN TRANSACTION CandidateDelete
    WITH MARK N'Deleting a Job Candidate';
GO
USE AdventureWorks2008R2;
GO
DELETE FROM AdventureWorks2008R2.HumanResources.JobCandidate
    WHERE JobCandidateID = 13;
GO
COMMIT TRANSACTION CandidateDelete;
GO


BEGIN DISTRIBUTED TRANSACTION;
-- Delete candidate from local instance.
DELETE AdventureWorks2008R2.HumanResources.JobCandidate
    WHERE JobCandidateID = 13;
-- Delete candidate from remote instance.
DELETE RemoteServer.AdventureWorks2008R2.HumanResources.JobCandidate
    WHERE JobCandidateID = 13;
COMMIT TRANSACTION;




BEGIN TRAN T1;
UPDATE table1 ...;
BEGIN TRAN M2 WITH MARK;
UPDATE table2 ...;
SELECT * from table1;
COMMIT TRAN M2;
UPDATE table3 ...;
COMMIT TRAN T1;




CREATE TABLE TestTran (Cola int PRIMARY KEY, Colb char(3));
GO
-- This statement sets @@TRANCOUNT to 1.
BEGIN TRANSACTION OuterTran;
GO
PRINT N'Transaction count after BEGIN OuterTran = '
    + CAST(@@TRANCOUNT AS nvarchar(10));
GO
INSERT INTO TestTran VALUES (1, 'aaa');
GO
-- This statement sets @@TRANCOUNT to 2.
BEGIN TRANSACTION Inner1;
GO
PRINT N'Transaction count after BEGIN Inner1 = '
    + CAST(@@TRANCOUNT AS nvarchar(10));
GO
INSERT INTO TestTran VALUES (2, 'bbb');
GO
-- This statement sets @@TRANCOUNT to 3.
BEGIN TRANSACTION Inner2;
GO
PRINT N'Transaction count after BEGIN Inner2 = '
    + CAST(@@TRANCOUNT AS nvarchar(10));
GO
INSERT INTO TestTran VALUES (3, 'ccc');
GO
-- This statement decrements @@TRANCOUNT to 2.
-- Nothing is committed.
COMMIT TRANSACTION Inner2;
GO
PRINT N'Transaction count after COMMIT Inner2 = '
    + CAST(@@TRANCOUNT AS nvarchar(10));
GO
-- This statement decrements @@TRANCOUNT to 1.
-- Nothing is committed.
COMMIT TRANSACTION Inner1;
GO
PRINT N'Transaction count after COMMIT Inner1 = '
    + CAST(@@TRANCOUNT AS nvarchar(10));
GO
-- This statement decrements @@TRANCOUNT to 0 and
-- commits outer transaction OuterTran.
COMMIT TRANSACTION OuterTran;
GO
PRINT N'Transaction count after COMMIT OuterTran = '
    + CAST(@@TRANCOUNT AS nvarchar(10));
GO


--
--The following example shows the effect of rolling back a named transaction.
ROLLBACK TRAN @TransactionName




  -- Detect whether the procedure was called
    -- from an active transaction and save
    -- that for later use.
    -- In the procedure, @TranCounter = 0
    -- means there was no active transaction
    -- and the procedure started one.
    -- @TranCounter > 0 means an active
    -- transaction was started before the 
    -- procedure was called.
    DECLARE @TranCounter INT;
    SET @TranCounter = @@TRANCOUNT;
    IF @TranCounter > 0
        -- Procedure called when there is
        -- an active transaction.
        -- Create a savepoint to be able
        -- to roll back only the work done
        -- in the procedure if there is an
        -- error.
        SAVE TRANSACTION ProcedureSave;
    ELSE
        -- Procedure must start its own
        -- transaction.
        BEGIN TRANSACTION;
    -- Modify database.
    BEGIN TRY
        DELETE HumanResources.JobCandidate
            WHERE JobCandidateID = @InputCandidateID;
        -- Get here if no errors; must commit
        -- any transaction started in the
        -- procedure, but not commit a transaction
        -- started before the transaction was called.
        IF @TranCounter = 0
            -- @TranCounter = 0 means no transaction was
            -- started before the procedure was called.
            -- The procedure must commit the transaction
            -- it started.
            COMMIT TRANSACTION;
    END TRY
    BEGIN CATCH
        -- An error occurred; must determine
        -- which type of rollback will roll
        -- back only the work done in the
        -- procedure.
        IF @TranCounter = 0
            -- Transaction started in procedure.
            -- Roll back complete transaction.
            ROLLBACK TRANSACTION;
        ELSE
            -- Transaction started before procedure
            -- called, do not roll back modifications
            -- made before the procedure was called.
            IF XACT_STATE() <> -1
                -- If the transaction is still valid, just
                -- roll back to the savepoint set at the
                -- start of the stored procedure.
                ROLLBACK TRANSACTION ProcedureSave;
                -- If the transaction is uncommitable, a
                -- rollback to the savepoint is not allowed
                -- because the savepoint rollback writes to
                -- the log. Just return to the caller, which
                -- should roll back the outer transaction.

        -- After the appropriate rollback, echo error
        -- information to the caller.
        DECLARE @ErrorMessage NVARCHAR(4000);

        SELECT @ErrorMessage = ERROR_MESSAGE();

        RAISERROR (@ErrorMessage, -- Message text.
                   @ErrorSeverity, -- Severity.
                   @ErrorState -- State.
                   );
    END CATCH
  
  SELECT BankerID, BankerName
INTO #BankerCopy
FROM Bankers
WHERE BankerID < 5
BEGIN TRAN
  DELETE #BankerCopy WHERE BankerID = 1
   SAVE TRAN Banker1
     DELETE #BankerCopy WHERE BankerID = 2
     SAVE TRAN Banker2
       DELETE #BankerCopy WHERE BankerID = 3
       SELECT * FROM #BankerCopy
     ROLLBACK TRAN Banker2
     SELECT * FROM #BankerCopy
   ROLLBACK TRAN Banker1
   SELECT * FROM #BankerCopy
 COMMIT TRAN
 GO


SET TRANSACTION ISOLATION LEVEL REPEATABLE READ;


@@TRANCOUNT

``` 



## Locking
``` sql 

SELECT resource_associated_entity_id, resource_type,
request_mode, request_session_id
FROM sys.dm_tran_locks

--This query identified that session 54 is blocking session 55.
SELECT blocking_session_id, wait_duration_ms, session_id
FROM sys.dm_os_waiting_tasks
WHERE blocking_session_id IS NOT NULL

SELECT t.text
FROM sys.dm_exec_connections c
CROSS APPLY sys.dm_exec_sql_text (c.most_recent_sql_handle) t
WHERE c.session_id = 54

--The timeout period is the number ofmilliseconds before a locking error will be returned.
SET LOCK_TIMEOUT 1000


DBCC TRACEOFF (1222, -1)
GO
DBCC TRACESTATUS
``` 



## UNION vs UNION ALL
Note: The UNION operator selects only distinct values by default. To allow duplicate values, use the ALL keyword with UNION.
``` sql 
SELECT column_name(s) FROM table1
UNION -- UNION ALL
SELECT column_name(s) FROM table2;
``` 



## SELECT INTO 
With SQL, you can copy information from one table into another.

The SELECT INTO statement copies data from one table and inserts it into a new table.
``` sql 

-- example creates a temporary table named #Bicycles in tempdb.
SELECT * 
INTO #Bicycles
FROM AdventureWorks2008R2.Production.Product

-- example creates the permanent table NewProducts.
SELECT * INTO dbo.NewProducts
FROM Production.Product
WHERE ListPrice > $25 


-- Create a backup copy of Customers:
SELECT *
INTO CustomersBackup2013
FROM Customers;

--Use the IN clause to copy the table into another database:
SELECT *
INTO CustomersBackup2013 IN 'Backup.mdb'
FROM Customers;




--Copy only a few columns into the new table:

SELECT CustomerName, ContactName
INTO CustomersBackup2013
FROM Customers;

--Copy only the German customers into the new table:
SELECT *
INTO CustomersBackup2013
FROM Customers
WHERE Country='Germany';

--Copy data from more than one table into the new table:
SELECT Customers.CustomerName, Orders.OrderID
INTO CustomersOrderBackup2013
FROM Customers
LEFT JOIN Orders
ON Customers.CustomerID=Orders.CustomerID;



Tip: The SELECT INTO statement can also be used to create a new, empty table using the schema of another. Just add a WHERE clause that causes the query to return no data:
SELECT *
INTO newtable
FROM table1
WHERE 1=0;


SELECT *
INTO newtable [IN externaldb]
FROM table1;


-- Create a new table with columns from the existing table Person.Address. A new IDENTITY
SELECT IDENTITY (int, 100, 5) AS AddressID, 
       a.AddressLine1, a.City,  a.PostalCode
INTO Person.USAddress 
FROM Person.Address AS a


-- Specify the remote data source in the FROM clause using a four-part name 
-- in the form linked_server.catalog.schema.object.
SELECT *
INTO dbo.Departments
FROM MyLinkServer.AdventureWorks2008R2.HumanResources.Department


-- Use the OPENQUERY function to access the remote data source.
SELECT *
INTO dbo.DepartmentsUsingOpenQuery
FROM OPENQUERY(MyLinkServer, 'SELECT *
               FROM AdventureWorks2008R2.HumanResources.Department'); 


-- Use the OPENDATASOURCE function to specify the remote data source.
-- Specify a valid server name for Data Source using the format server_name or server_name\instance_name.
SELECT *
INTO dbo.DepartmentsUsingOpenDataSource
FROM OPENDATASOURCE('SQLNCLI',
    'Data Source=server_name;Integrated Security=SSPI')
    .AdventureWorks2008R2.HumanResources.Department;               



-- Creating a table by specifying columns from a remote data source
SELECT *
INTO dbo.Departments
FROM MyLinkServer.AdventureWorks2008R2.HumanResources.Department
GO

-- Use the OPENQUERY function to access the remote data source.
SELECT *
INTO dbo.DepartmentsUsingOpenQuery
FROM OPENQUERY(MyLinkServer, 'SELECT * FROM AdventureWorks2008R2.HumanResources.Department'); 
GO
-- Use the OPENDATASOURCE function to specify the remote data source.
-- Specify a valid server name for Data Source using the format server_name or server_name\instance_name.
SELECT *
INTO dbo.DepartmentsUsingOpenDataSource
FROM OPENDATASOURCE('SQLNCLI','Data Source=server_name;Integrated Security=SSPI')
    .AdventureWorks2008R2.HumanResources.Department;
GO


--Creating an identity column using the IDENTITY function
SELECT IDENTITY (int, 100, 5) AS AddressID, a.AddressLine1, a.City, b.Name AS State, 
INTO Person.USAddress 
FROM Person.Address 


--Quickly Copy the stucture
--Although the structure of the selected columns is reproduced, the constraints, indexes, and other separate
--objects dependent on the source table are not copied.
SELECT *
INTO Store_Archive_2
FROM Sales.Store
WHERE 1=0


``` 

## INSERT INTO SELECT Statement
With SQL, you can copy information from one table into another.

The INSERT INTO SELECT statement copies data from one table and inserts it into an existing table.



``` sql 
INSERT INTO table2 
SELECT * FROM table1;


INSERT INTO Customers (CustomerName, Country)
SELECT SupplierName, Country FROM Suppliers;


INSERT INTO Customers (CustomerName, Country)
SELECT SupplierName, Country FROM Suppliers
WHERE Country='Germany';

``` 


## CREATE Database

``` sql 

``` 



## Tables
In SQL, we have the following constraints:

* NOT NULL - Indicates that a column cannot store NULL value
* UNIQUE - Ensures that each row for a column must have a unique value
* PRIMARY KEY - A combination of a NOT NULL and UNIQUE. Ensures that a column (or combination of two or more columns) have a unique identity which helps to find a particular record in a table more easily and quickly
* FOREIGN KEY - Ensure the referential integrity of the data in one table to match values in another table
* CHECK - Ensures that the value in a column meets a specific condition
* DEFAULT - Specifies a default value for a column

* [Read detail](https://msdn.microsoft.com/en-us/library/ms174979.aspx)
* 
``` sql 
--------------------------------------------------------
-- Drop table if exists
--------------------------------------------------------
IF OBJECT_ID('dbo.Scores', 'U') IS NOT NULL 
  DROP TABLE dbo.Scores; 

--------------------------------------------------------
-- Create Table
--------------------------------------------------------
CREATE TABLE dbo.PurchaseOrderDetail  
(  
	-- identity column
	RowID [int] IDENTITY(1,1) NOT NULL,

	--Create a PRIMARY KEY constraint on a column
	EmployeeID int NOT NULL PRIMARY KEY CLUSTERED
	
	--Using FOREIGN KEY constraints
	SalesPersonID int NULL  REFERENCES SalesPerson(SalesPersonID) 

	--You can also explicitly use the FOREIGN KEY clause and restate the column attribute.
	--FOREIGN KEY (SalesPersonID) REFERENCES SalesPerson(SalesPersonID)
	
	--Multicolumn key constraints are created as table constraints. 
	--CONSTRAINT FK_SpecialOfferProduct_SalesOrderDetail FOREIGN KEY  (ProductID, SpecialOfferID)  REFERENCES SpecialOfferProduct (ProductID, SpecialOfferID)  

    --UNIQUE constraints are used to enforce uniqueness on nonprimary key columns. 
	Name nvarchar(100) NOT NULL  UNIQUE NONCLUSTERED  

	--Using DEFAULT definitions
	CreatedDate Datetime DEFAULT (getdate())  
	
	--Using CHECK constraints
	CreditRating INT CHECK (CreditRating >= 1 and CreditRating <= 5) 
	
	--CONSTRAINT CK_emp_id CHECK (emp_id LIKE    '[A-Z][A-Z][A-Z][1-9][0-9]')  

	--Creating a table with an xml column typed to an XML schema collection
	Resume xml( DOCUMENT HumanResources.HRResumeSchemaCollection)
	
	--Creating a computed column based on a user-defined type column
	 u utf8string
	 
    --Using an expression for a computed column
	TotalPrice AS (UnitPrice + OrderQty)

	--Using the USER_NAME function for a computed column
	myuser_name AS USER_NAME()
	
	--Creating a table that has sparse columns 
	--So when should you use a Sparse Column? When you expect a significant percentage of the rows to have a NULL value. Some examples that come to mind:
	c2 varchar(50) SPARSE NULL 
	
	--Creating a table that has a FILESTREAM column
	Photo varbinary(max) FILESTREAM NULL  
	
	--The UNIQUEIDENTIFIER along with ROWGUIDCOL NEWSEQUENTIALID() is far more efficient than normal UNIQUEIDENTIFIER along with NEWID().
	ID UNIQUEIDENTIFIER ROWGUIDCOL PRIMARY KEY DEFAULT NEWSEQUENTIALID()
	
	--New column using  NEWID()  
	MyRowGuidColumn uniqueidentifier NOT NULL ROWGUIDCOL  UNIQUE DEFAULT NEWID()  
		
    -- CONSTRAINT column
    ModifiedDate datetime NOT NULL  CONSTRAINT DF_PurchaseOrderDetail_ModifiedDate DEFAULT (getdate()),  
    
    
    CONSTRAINT PK_PurchaseOrderDetail_PurchaseOrderID_LineNumber  PRIMARY KEY CLUSTERED (PurchaseOrderID, LineNumber)  

)   
WITH (
PAD_INDEX  = OFF, STATISTICS_NORECOMPUTE  = OFF, IGNORE_DUP_KEY = OFF
IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS  = ON, ALLOW_PAGE_LOCKS  = ON,
DATA_COMPRESSION = ROW,
SYSTEM_VERSIONING = ON,  MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA,
) ON [PRIMARY]

--------------------------------------------------------
-- Alter Table
--------------------------------------------------------
--dding a new column
ALTER TABLE Persons ADD DateOfBirth date

--DROP COLUMN Example
ALTER TABLE Persons DROP COLUMN DateOfBirth

-- Remove multiple columns.
ALTER TABLE dbo.doc_exb DROP COLUMN column_c, column_d;

-- Change Data Type Example
ALTER TABLE Persons ALTER COLUMN DateOfBirth year

--Rename column in table
sp_rename 'table_name.old_column', 'new_name', 'COLUMN';

--Add multiple columns in table
ALTER TABLE supplier
  ADD (supplier_name char(50), city char(45));


--Adding a column with a constraint       
ALTER TABLE CUSTOMERS    ADD CONSTRAINT myCheckConstraint CHECK(AGE >= 18);
   
-- Adding an unverified CHECK constraint to an existing column
ALTER TABLE dbo.doc_exd WITH NOCHECK  ADD CONSTRAINT exd_check CHECK (column_a > 1) ;

--Adding a DEFAULT constraint to an existing column
ALTER TABLE dbo.doc_exz ADD CONSTRAINT col_b_def DEFAULT 50 FOR column_b ;

--Adding a nullable column with default values
ALTER TABLE dbo.doc_exf  ADD AddDate smalldatetime NULL CONSTRAINT AddDateDflt DEFAULT GETDATE() WITH VALUES ;   

--Creating a PRIMARY KEY constraint with index options
ALTER TABLE Production.TransactionHistoryArchive WITH NOCHECK 
ADD CONSTRAINT PK_TransactionHistoryArchive_TransactionID PRIMARY KEY CLUSTERED (TransactionID)
WITH (FILLFACTOR = 75, ONLINE = ON, PAD_INDEX = ON);

--Adding an encrypted column   
ALTER TABLE Customers ADD
    PromotionCode nvarchar(100) 
    ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = MyCEK,
    ENCRYPTION_TYPE = RANDOMIZED,
    ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') ;
    
--Dropping constraints and columns    
ALTER TABLE CUSTOMERS	 DROP CONSTRAINT myCheckConstraint; 	

-- Example 2. Remove two constraints and one column	
ALTER TABLE dbo.doc_exc    DROP CONSTRAINT CONSTRAINT my_constraint, my_pk_constraint, COLUMN column_b ;	


--Dropping a PRIMARY KEY constraint in the ONLINE mode
ALTER TABLE Production.TransactionHistoryArchive DROP CONSTRAINT PK_TransactionHistoryArchive_TransactionID WITH (ONLINE = ON);

--A. Modifying a table to change the compression
ALTER TABLE T1  REBUILD WITH (DATA_COMPRESSION = PAGE);


--Configuring change tracking on a table
ALTER TABLE Person.Person ENABLE CHANGE_TRACKING;
ALTER TABLE Person.Person ENABLE CHANGE_TRACKING WITH (TRACK_COLUMNS_UPDATED = ON)

ALTER TABLE Person.Person DISABLE CHANGE_TRACKING;

-- Disable the constraint and try again.
ALTER TABLE dbo.cnst_example NOCHECK CONSTRAINT salary_cap;

-- Re-enable the constraint and try another insert; this will fail.
ALTER TABLE dbo.cnst_example CHECK CONSTRAINT salary_cap;

--Disabling and re-enabling a trigger
ALTER TABLE dbo.trig_example DISABLE TRIGGER trig1 ;

-- Re-enable the trigger.
ALTER TABLE dbo.trig_example ENABLE TRIGGER trig1 ;


``` 


## Index

``` sql 

----------------------------------------------
-- Drop index if exists
----------------------------------------------
IF EXISTS (SELECT name FROM sys.indexes WHERE name = N'IX_ProductVendor_VendorID')  
DROP INDEX IX_ProductVendor_VendorID ON Purchasing.ProductVendor;  
  
----------------------------------------------
-- Create index 
----------------------------------------------
  
-- Create a nonclustered index on a table or view  
CREATE INDEX IX_VendorID ON ProductVendor (VendorID);  
CREATE INDEX IX_VendorID ON dbo.ProductVendor (VendorID DESC, Name ASC, Address DESC);  
--Rebuild and add the OrganizationKey  
CREATE INDEX IX_FF ON dbo.FactFinance ( FinanceKey, DateKey, OrganizationKey DESC)   WITH ( DROP_EXISTING = ON );  

--Create a simple nonclustered onMultiple Columns
CREATE NONCLUSTERED INDEX IX_SalesPerson_SalesQuota_SalesYTD ON Sales.SalesPerson (SalesQuota, SalesYTD);  

--Create an index on a table in another database
CREATE CLUSTERED INDEX IX_ProductVendor_VendorID ON Purchasing..ProductVendor (VendorID); 

--Create a unique nonclustered index
 CREATE UNIQUE INDEX AK_UnitMeasure_Name ON Production.UnitMeasure(Name);  
    
-- Use the IGNORE_DUP_KEY option
CREATE UNIQUE INDEX AK_Index ON #Test (C2) WITH (IGNORE_DUP_KEY = ON);  
                        
-- Using DROP_EXISTING to drop and re-create an index     
CREATE NONCLUSTERED INDEX IX_WorkOrder_ProductID ON Production.WorkOrder(ProductID)  
    WITH (FILLFACTOR = 80, PAD_INDEX = ON,   DROP_EXISTING = ON);  
 
-- Create a partitioned index                
CREATE NONCLUSTERED INDEX IX_TransactionHistory_ReferenceOrderID  
    ON Production.TransactionHistory (ReferenceOrderID)  
    ON TransactionsPS1 (TransactionDate);  
    
--Create an index with included (non-key) columns
CREATE NONCLUSTERED INDEX IX_Address_PostalCode  
    ON Person.Address (PostalCode)  
    INCLUDE (AddressLine1, AddressLine2, City, StateProvinceID);  
   

-- Creating a filtered index or Indexing a Subset of Rows
CREATE NONCLUSTERED INDEX NCI_UnitPrice_SalesOrderDetail
ON Sales.SalesOrderDetail(UnitPrice)
WHERE UnitPrice >= 150.00 AND UnitPrice <= 175.00
   
--Using PAD_INDEX and FILLFACTOR
CREATE NONCLUSTERED INDEX NI_TerminationReason_TerminationReason_DepartmentID
ON HumanResources.TerminationReason
(TerminationReason ASC, DepartmentID ASC)
WITH (PAD_INDEX=ON, FILLFACTOR=50)
 
   

--Reducing Index Size
CREATE NONCLUSTERED INDEX NCI_SalesOrderDetail ON Sales.SalesOrderDetail (CarrierTrackingNumber) WITH (DATA_COMPRESSION = PAGE)
--Create a compressed index
CREATE NONCLUSTERED INDEX IX_INDEX_1  ON T1 (C2)   WITH ( DATA_COMPRESSION = ROW ) ;

CREATE CLUSTERED INDEX IX_PartTab2Col1  ON PartitionTable1 (Col1)   WITH (DATA_COMPRESSION = PAGE ON PARTITIONS(1),    DATA_COMPRESSION = ROW ON PARTITIONS (2 TO 4 ) ) ;  

--Allowing User Table Access During Index Creation
CREATE NONCLUSTERED INDEX NCI_ProductVendor_MinOrderQty ON Purchasing.ProductVendor(MinOrderQty) WITH (ONLINE = ON)

-- Disable page locks. Table and row locks can still be used.
CREATE INDEX NI_EmployeePayHistory_Rate ON HumanResources.EmployeePayHistory (Rate) WITH (ALLOW_PAGE_LOCKS=OFF)

----------------------------------------------
-- Viewing IndexMeta Data
----------------------------------------------

SELECT SUBSTRING(name, 1,30) index_name,
allow_row_locks,
allow_page_locks,
is_disabled,
fill_factor,
has_filter
FROM sys.indexes
WHERE object_id = OBJECT_ID('HumanResources.Employee')

----------------------------------------------
-- Alter Index
----------------------------------------------

--Disabling an Index
ALTER INDEX UNI_TerminationReason ON HumanResources.TerminationReason DISABLE

----------------------------------------------
-- Dropping Indexes
----------------------------------------------
DROP INDEX HumanResources.TerminationReason.UNI_TerminationReason

``` 



## DROP

``` sql 
DROP INDEX table_name.index_name
DROP TABLE table_name
DROP DATABASE database_name

``` 

## ALTER Statements

``` sql 
ALTER TABLE table_name
ADD column_name datatype


ALTER TABLE table_name
DROP COLUMN column_name


--To change the data type of a column in a table
ALTER TABLE table_name
ALTER COLUMN column_name datatype
``` 







## Stored Procedure

``` sql 
----------------------------------------------
-- Create Procedure
----------------------------------------------

IF OBJECT_ID ( 'dbo.usp_UPD_ShoppingCartItem', 'P' ) IS NOT NULL 
    DROP PROCEDURE dbo.usp_UPD_ShoppingCartItem;
GO

CREATE PROCEDURE dbo.usp_UPD_ShoppingCartItem
(   @ShoppingCartID nvarchar(50),
    @Quantity int = 1, -- defaulted to quantity of 1
    @ProductID int,
    @DeptCount int OUTPUT)
WITH ENCRYPTION
WITH RECOMPILE -- Plan will never be saved --Option 1 for SP recomplile
WITH EXECUTE AS 'CompanyDomain\SqlUser1'    -- { CALLER | SELF | OWNER | 'user_name' }
AS
    -- Otherwise insert a new row
    INSERT Sales.ShoppingCartItem
    (ShoppingCartID, ProductID, Quantity)
    VALUES (@ShoppingCartID, @ProductID, @Quantity)

    PRINT 'INSERT performed. '

    SELECT @DeptCount = @@ROWCOUNT
    
    RETURN 2;

END
GO


----------------------------------------------
-- Drop Procedure
----------------------------------------------
DROP PROCEDURE dbo.usp_SEL_Department

----------------------------------------------
-- the sp_procoption stored procedure is used to set this new procedure to execute when the SQL Server service restarts
----------------------------------------------


-- Use the EXECUTE AS CALLER stand-alone statement 
CREATE PROCEDURE dbo.usp_Demo
WITH EXECUTE AS 'SqlUser1'
AS
SELECT user_name(); -- Shows execution context is set to SqlUser1.
EXECUTE AS CALLER;
SELECT user_name(); -- Shows execution context is set to SqlUser2, the caller of the module.
REVERT;
SELECT user_name(); -- Shows execution context is set to SqlUser1.
GO


EXECUTE AS
https://technet.microsoft.com/en-us/library/ms178106(v=sql.105).aspx


----------------------------------------------
-- Execute Procedure
----------------------------------------------

EXEC usp_UPD_ShoppingCartItem 

--Using EXECUTE to pass a single parameter
EXEC dbo.uspGetEmployeeManagers 6;

--Using multiple parameters
EXEC dbo.uspGetWhereUsedProductID 819, @CheckDate;

--The variable can be explicitly named in the execution:
EXEC dbo.uspGetEmployeeManagers @BusinessEntityID = 6;

--This needs to match the SP parameter order, position in important
EXEC usp_UPD_ShoppingCartItem '1255', 2, 316

EXEC Sp_MyProg  @ID OUTPUT, '2013-10-10', 'P%'

-- position in not important, order doesn't matter. 
-- Parameter is optional, if SP allowed it
EXEC Sp_MyProg  @ID = @MyInvTotal OUTPUT, @DataVar = '2013-10-10', @VandorVAR = 'P%'

EXEC sp_recompile 'Person.Address';


DECLARE @return_status int;
EXEC @return_status = checkstate '2';
SELECT 'Return Status' = @return_status;


--Using EXECUTE with a Character String
USE master; EXEC ('USE AdventureWorks2008R2; SELECT BusinessEntityID, JobTitle FROM HumanResources.Employee;');

--Using EXECUTE with a remote stored procedure
EXECUTE @retstat = SQLSERVER1.AdventureWorks2008R2.dbo.uspGetEmployeeManagers @BusinessEntityID = 6;

--Using EXECUTE with a stored procedure variable
DECLARE @proc_name varchar(30) = 'sys.sp_who';
EXEC @proc_name;


-- Using the DEFAULT keyword for the first parameter.
EXECUTE dbo.ProcTestDefaults @p1 = DEFAULT, @p2 = 'D';
-- Specifying the parameters in an order different from the order defined in the procedure.
EXECUTE dbo.ProcTestDefaults DEFAULT, @p3 = 'Local', @p2 = 'E';
-- Using the DEFAULT keyword for the first and third parameters.
EXECUTE dbo.ProcTestDefaults DEFAULT, 'H', DEFAULT;

--H. Using EXECUTE WITH RECOMPILE
EXECUTE dbo.Proc_Test_Defaults @p2 = 'A' WITH RECOMPILE;

--I. Using EXECUTE with a user-defined function
--example executes the ufnGetSalesOrderStatusText scalar user-defined function. It uses the variable @returnstatus to store the value returned by the function. The function expects one input parameter, @Status. This is defined as a tinyint data type.
EXEC @returnstatus = dbo.ufnGetSalesOrderStatusText @Status = 2;


--J. Using EXECUTE to query an Oracle database on a linked server
-- Setup the linked server.
EXEC sp_addlinkedserver  
        @server='ORACLE',
        @srvproduct='Oracle',
        @provider='OraOLEDB.Oracle', 
        @datasrc='ORACLE10';

EXEC sp_addlinkedsrvlogin 
    @rmtsrvname='ORACLE',
    @useself='false', 
    @locallogin=null, 
    @rmtuser='scott', 
    @rmtpassword='tiger';
 
EXEC sp_serveroption 'ORACLE', 'rpc out', true;
GO
 
-- Execute several statements on the linked Oracle server.
EXEC ( 'SELECT * FROM scott.emp') AT ORACLE;
GO
EXEC ( 'SELECT * FROM scott.emp WHERE MGR = ?', 7902) AT ORACLE;
GO
DECLARE @v INT; 
SET @v = 7902;
EXEC ( 'SELECT * FROM scott.emp WHERE MGR = ?', @v) AT ORACLE;
GO


--K. Using EXECUTE AS USER to switch context to another user
EXECUTE ('CREATE TABLE Sales.SalesTable (SalesID int, SalesName varchar(10));')
AS USER = 'User1';

--L. Using a parameter with EXECUTE and AT linked_server_name
-- Setup the linked server.
EXEC sp_addlinkedserver 'SeattleSales', 'SQL Server'
GO
-- Execute the SELECT statement.
EXECUTE ('SELECT ProductID, Name FROM AdventureWorks2008R2.Production.Product WHERE ProductID = ? ', 952) AT SeattleSales;
GO



``` 

## Cursor

``` sql 

-- I won't show rowcounts in the results
SET NOCOUNT ON
DECLARE @session_id smallint

-- Declare the cursor
DECLARE session_cursor CURSOR
FORWARD_ONLY READ_ONLY
FOR SELECT session_id
FROM sys.dm_exec_requests
WHERE status IN ('runnable', 'sleeping', 'running')

-- Open the cursor
OPEN session_cursor

-- Retrieve one row at a time from the cursor
FETCH NEXT
FROM session_cursor
INTO @session_id

-- Keep retrieving rows while the cursor has them
WHILE @@FETCH_STATUS = 0
BEGIN
	PRINT 'Spid #: ' + STR(@session_id)
	EXEC ('DBCC OUTPUTBUFFER (' + @session_id + ')')
	-- Grab the next row
	FETCH NEXT
	FROM session_cursor
	INTO @session_id
END

-- Close the cursor
CLOSE session_cursor

-- Deallocate the cursor
DEALLOCATE session_cursor

``` 

## Inbuild Functions

``` sql 

--returns the number of characters in the Unicode string
SELECT LEN(N'She sells sea shells by the sea shore.')	-- 38

returns the number of bytes in the Unicode string:
SELECT DATALENGTH(N'She sells sea shells by the sea shore.') --76


SELECT REPLACE('Zenon is our major profit center. Zenon leads the way.', 'Zenon', 'Xerxes')


SELECT STUFF ( 'My cat''s name is X. Have you met him?',
18,
1,
'Edgar' )
This returns

SELECT LOWER(DocumentSummary)
SELECT UPPER(DocumentSummary)

SELECT RTRIM('"' + 'String with trailing blanks ') + '"'


SELECT REPLICATE ('Z', 30)	--ZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZ

SELECT 'Give me some' + SPACE(6) + 'space.'

SELECT TOP 1
GroupName,
REVERSE(GroupName)

SUBSTRING ( expression, start, length )


Working with NULLs
Replacing a NULLValue with an AlternativeValue
ISNULL(BusinessEntityID, 0)

--returns the first non-NULL value froma provided list of expressions
SELECT COALESCE(@null, 10, 24)

--NULLIF returns a NULL value when the two provided expressions have the same value; otherwise, the first expression is returned.
SELECT NULLIF(10, 20) -- 10
SELECT NULLIF(10, 10) -- NULL


SELECT 'CurrDateAndTime_HighPrecision', SYSDATETIME()
SELECT 'UniversalTimeCoordinate_HighPrecision', SYSUTCDATETIME()
SELECT 'CurrDateAndTime_HighPrecision _UTC_Adjust', SYSDATETIMEOFFSET()

--Converting Between Time Zones
SELECT SWITCHOFFSET ( '2007-08-12 09:43:25.9783262 -05:00', '+03:00')
SELECT TODATETIMEOFFSET ( '2007-08-12 09:43:25' , '-05:00' )

--decreases a date by sixmonths
SELECT DATEADD(mm, -6, '4/2/2009')	--2008-10-02 00:00:00.000
SELECT DATEADD(d, 50, '4/2/2009')	--2009-05-22 00:00:00.000
SELECT DATEADD(mi, -30, '2009-09-01 23:30:00.000')	--2009-09-01 23:00:00.000

SELECT ProductID,
GETDATE() Today,
EndDate,
DATEDIFF(m, EndDate, GETDATE())

-Displaying the StringValue for Part of a Date
DATENAME ( datepart , date )

SELECT DATEPART(yy, GETDATE())	-- 2008
SELECT DATEPART(m, GETDATE())	-- 2


SELECT YEAR(GETDATE())		-- 2008
SELECT MONTH(GETDATE())		-- 9
SELECT DAY(GETDATE())		-- 30

SELECT CONVERT(char(4), 2008) + ' Can now be concatenated!'
SELECT BusinessEntityID, CAST(SickLeaveHours AS char(4))


-- Returns 0
SELECT ISNUMERIC('123ABC')
-- Returns 1
SELECT ISNUMERIC('123')
``` 

## Views

``` sql 

------------------------------------------------------
-- Drop if exists
------------------------------------------------------

IF OBJECT_ID ('hiredate_view', 'V') IS NOT NULL
DROP VIEW hiredate_view ;
GO

------------------------------------------------------
-- Regular view
------------------------------------------------------

--Using a simple CREATE VIEW
CREATE VIEW hiredate_view
AS 
SELECT p.FirstName, p.LastName, e.BusinessEntityID, e.HireDate
FROM HumanResources.Employee e 

--Using WITH ENCRYPTION
CREATE VIEW Purchasing.PurchaseOrderReject
WITH ENCRYPTION
AS
SELECT PurchaseOrderID, ReceivedQty, RejectedQty, 
    RejectedQty / ReceivedQty AS RejectRatio, DueDate
FROM Purchasing.PurchaseOrderDetail


--Using WITH CHECK OPTION
-- It  shows a view named SeattleOnly that references five tables and allows for data modifications to apply only to employees who live in Seattle.
CREATE VIEW dbo.SeattleOnly
AS
SELECT p.LastName, p.FirstName, e.JobTitle, a.City, sp.StateProvinceCode
FROM HumanResources.Employee e
INNER JOIN Person.Person p
ON p.BusinessEntityID = e.BusinessEntityID
    INNER JOIN Person.BusinessEntityAddress bea 
    ON bea.BusinessEntityID = e.BusinessEntityID 
    INNER JOIN Person.Address a 
    ON a.AddressID = bea.AddressID
    INNER JOIN Person.StateProvince sp 
    ON sp.StateProvinceID = a.StateProvinceID
WHERE a.City = 'Seattle'
WITH CHECK OPTION ;
GO


-------------------------------------------------
--Creating an IndexedView
-------------------------------------------------
CREATE VIEW dbo.v_Product_Sales_By_LineTotal
WITH SCHEMABINDING
AS
SELECT p.ProductID, p.Name ProductName,
SUM(LineTotal) LineTotalByProduct,
COUNT_BIG(*) LineItems
FROM Sales.SalesOrderDetail s
INNER JOIN Production.Product p ON
s.ProductID = p.ProductID
GROUP BY p.ProductID, p.Name

CREATE UNIQUE CLUSTERED INDEX UCI_v_Product_Sales_By_LineTotal ON dbo.v_Product_Sales_By_LineTotal (ProductID)

Once the clustered index is created, I can then start creating nonclustered indexes as needed:
CREATE NONCLUSTERED INDEX NI_v_Product_Sales_By_LineTotal
ON dbo.v_Product_Sales_By_LineTotal (ProductName)
GO

SELECT TOP 5 ProductName, LineTotalByProduct
FROM v_Product_Sales_By_LineTotal
ORDER BY LineTotalByProduct DESC


SELECT ProductID
FROM dbo.v_Product_Sales_By_LineTotal
WITH (NOEXPAND, INDEX(NI_v_Product_Sales_By_LineTotal))
WHERE ProductName = 'Short-Sleeve Classic Jersey, L'


------------------------------------------------------
-- Partitioned Views
------------------------------------------------------
--Creating a Distributed-PartitionedView
CREATE VIEW dbo.v_WebHits AS
	SELECT WebHitID,
	WebSite,
	HitDT
	FROM TSQLRecipeTest.dbo.WebHits_MegaCorp
UNION ALL
	SELECT WebHitID,
	WebSite,
	HitDT
	FROM JOEPROD.TSQLRecipeTest.dbo.WebHits_MiniCorp
	

------------------------------------------------------
-- Modifying Data Through aView
------------------------------------------------------	
	
CREATE VIEW Production.vw_Location
AS
SELECT LocationID,
Name LocationName,
CostRate,
Availability,
CostRate/Availability CostToAvailabilityRatio
FROM Production.Location
GO

--This next insert is attempted, this time only referencing the columns that exist in the base table:
INSERT Production.vw_Location (LocationName, CostRate, Availability)
VALUES ('Finishing Cabinet', 1.22, 75.00)


------------------------------------------------------
-- alter View
------------------------------------------------------	
ALTER VIEW dbo.v_Product_TransactionHistory
AS
SELECT p.Name,
p.ProductNumber,
t.TransactionID,
t.TransactionDate,
FROM Production.TransactionHistory t
INNER JOIN Production.Product p ON
t.ProductID = p.ProductID
GO

------------------------------------------------------
-- Dropping aView
------------------------------------------------------	
DROP VIEW dbo.v_Product_TransactionHistory



	
------------------------------------------------------
-- View Definition
------------------------------------------------------	
	
--Querying theView Definition
SELECT definition FROM sys.sql_modules
WHERE object_id = OBJECT_ID('v_Product_TransactionHistory')

SELECT OBJECT_DEFINITION ( OBJECT_ID('v_Product_TransactionHistory'))

--DisplayingViews and Their Structures
SELECT s.name SchemaName,
v.name ViewName
FROM sys.views v
INNER JOIN sys.schemas s ON
v.schema_id = s.schema_id
ORDER BY s.name,
v.name


SELECT v.name ViewName,
c.name ColumnName
FROM sys.columns c
INNER JOIN sys.views v ON
c.object_id = v.object_id
ORDER BY v.name,
c.name

--The first query in the recipe references the object catalog views sys.views and sys.schemas to return all views in the database:
FROM sys.views v
INNER JOIN sys.schemas s ON
v.schema_id = s.schema_id

--The second query reports on all columns returned by each view by querying the object catalog views sys.columns and sys.views:
FROM sys.columns c
INNER JOIN sys.views v ON
c.object_id = v.object_id

--Refreshing aView’s Definition
EXEC sp_refreshview 'dbo.v_Product_TransactionHistory'

EXEC sys.sp_refreshsqlmodule @name = 'dbo.v_Product_TransactionHistory'




``` 



## Common Table Expressions - CTE

``` sql 
----------------------------------------------
-- Sample 1
----------------------------------------------
-- Define the CTE expression name and column list.
WITH ProductsCTE(ProdName1,Price1) AS
-- Define the CTE query.
( SELECT ProductDesc,Price
  FROM PRODUCTS
  WHERE Price>20.00
)
-- Define the outer query referencing the CTE name.
SELECT ProdName1, Price1 FROM ProductsCTE

----------------------------------------------
-- Sample 2
----------------------------------------------
WITH MadridCusts AS
(
  SELECT ID=CustomerID, Company=CompanyName
  FROM Customers
)
SELECT ID,Company,Contact,Phone FROM MadridCusts

----------------------------------------------
-- You can define several CTEs that build upon each other.
----------------------------------------------
with USACustomers as
(
  select CustomerID,CompanyName,ContactName,Region,City,Phone,PostalCode
  from Customers
  where Country='USA'
)
,USACustomersInOregon as
(
  select * from USACustomers
  where Region='CA'
)
,FremeontCustomersInCalifornia as
(
  select *   from USACustomersInOregon
  where City='Fremont'
)
select * from FremeontCustomersInCalifornia

--Each CTE uses the result of the previous to continue to narrow down the result set. 
-- But since each CTE is treated as a view, the query optimizer is able to “push” the predicates into a single one. 
-- It is exactly the same in every aspect as the following query:

select CustomerID,CompanyName,ContactName,Region,City,Phone,PostalCode
from Customers
where Country='USA' and Region='CA' and City='Portland'


----------------------------------------------
--Updating and Deleting using CTE
--they are updatable.
----------------------------------------------
with USACustomers as
(
  select CustomerID,CompanyName,ContactName,Region,City,Phone,PostalCode,UpdateColumn
  from #Custs
  where Country='USA'
)
update USACustomers set UpdateColumn='X'

----------------------------------------------
--Generating Numbers
----------------------------------------------

--Generating Numbers
with 
  L0(c) as (select 0 from (values (0),(0),(0)) f(c)) --3 Rows
 ,L1(c) as (select 0 from L0 a,L0 b,L0 c)            --27 Rows (3x3x3)
 ,L2(c) as (select 0 from L1 a,L1 b,L1 c)            --19683 Rows (27x27x27)
 ,L3(c) as (select 0 from L2 a,L2 b)                 --387,420,489 Rows (19683x19683)
 ,NN(n) as (select row_number() over (order by (select 0)) from L3)
select n into #Nums from NN where n<=1000000


----------------------------------------------
-- Create new column and update with row number for each row using CTE
-- Create RowID and RowOrder column, RowOrder should be 1.
----------------------------------------------
WITH Temp_STAGING_INASUP
AS
(
	--RowOrder is 1 for all row, records
	SELECT *, ROW_NUMBER() OVER(ORDER BY RowOrder) AS RowNumber FROM STAGING_INASUP
)
UPDATE Temp_STAGING_INASUP SET RowID = RowNumber



----------------------------------------------
--multiple CTEs calls from one single query
----------------------------------------------

WITH StudCTE(RollNo,StudentName,TeacherID) 
AS ( 
	SELECT ID,Name,TID FROM Student), 
	TeacherCTE(TID,TeacherName)
AS( 
	SELECT ID,Name FROM Teacher )

SELECT RollNo,StudentName,TeacherName FROM StudCTE SC 
INNER JOIN TeacherCTE TC ON SC.TeacherID=TC.TID


----------------------------------------------
--For removing the duplicate employee
----------------------------------------------
WITH EliminateDup(Eid,Name,Dept,RowID) AS
(
SELECT Eid,Ename,Dept, ROW_NUMBER()OVER(PARTITION BY Ename,Dept ORDER BY EID)AS RowID
FROM EMP
)
DELETE FROM EliminateDup WHERE RID>1

----------------------------------------------
--Recursion
----------------------------------------------
DECLARE @T VARCHAR(100)='Where,there,is,a,will,there,is,a,way'
SET @T =@T+','

;WITH MyCTE(Start,[End]) AS(
SELECT 1 AS Start,CHARINDEX(',',@T,1) AS [End]
UNION ALL
SELECT [End]+1 AS Start,CHARINDEX(',',@T,[End]+1)AS [End] from MyCTE where [End]<LEN(@T)
)
Select Start,[End],SUBSTRING(@T,Start,[End]-Start)AS String from MyCTE;

----------------------------------------------
-- recursively enumerate hierarchical data
----------------------------------------------
WITH ShowMessage(STATEMENT, LENGTH)
AS
(
SELECT STATEMENT = CAST('I Like ' AS VARCHAR(300)), LEN('I Like ')
UNION ALL
SELECT
      CAST(STATEMENT + 'CodeProject! ' AS VARCHAR(300))
      , LEN(STATEMENT) FROM ShowMessage
WHERE LENGTH < 300
)
SELECT STATEMENT, LENGTH FROM ShowMessage


----------------------------------------------
--D. Using a recursive common table expression to display two levels of recursion
----------------------------------------------

USE AdventureWorks2008R2;
GO
WITH DirectReports(ManagerID, EmployeeID, Title, EmployeeLevel) AS 
(
    SELECT ManagerID, EmployeeID, Title, 0 AS EmployeeLevel
    FROM dbo.MyEmployees 
    WHERE ManagerID IS NULL
    UNION ALL
    SELECT e.ManagerID, e.EmployeeID, e.Title, EmployeeLevel + 1
    FROM dbo.MyEmployees AS e
        INNER JOIN DirectReports AS d
        ON e.ManagerID = d.EmployeeID 
)
SELECT ManagerID, EmployeeID, Title, EmployeeLevel 
FROM DirectReports
WHERE EmployeeLevel <= 2 ;
GO


----------------------------------------------
--F. Using MAXRECURSION to cancel a statement
----------------------------------------------
--Creates an infinite loop
WITH cte (EmployeeID, ManagerID, Title) as
(
    SELECT EmployeeID, ManagerID, Title
    FROM dbo.MyEmployees
    WHERE ManagerID IS NOT NULL
  UNION ALL
    SELECT cte.EmployeeID, cte.ManagerID, cte.Title
    FROM cte 
    JOIN  dbo.MyEmployees AS e 
        ON cte.ManagerID = e.EmployeeID
)
--Uses MAXRECURSION to limit the recursive levels to 2
SELECT EmployeeID, ManagerID, Title
FROM cte
OPTION (MAXRECURSION 2);


----------------------------------------------
--F. Combine select statement
----------------------------------------------
WITH VendorSearch (RowNumber, VendorName, AccountNumber)
AS
(
    SELECT ROW_NUMBER() OVER (ORDER BY Name) RowNum,
    Name,
    AccountNumber
    FROM Purchasing.Vendor
)
SELECT RowNumber, VendorName, AccountNumber FROM VendorSearch
WHERE RowNumber BETWEEN 1 AND 5
UNION
SELECT RowNumber, VendorName, AccountNumber FROM VendorSearch
WHERE RowNumber BETWEEN 100 AND 104



``` 


## User Defined Functions

* There are three different types of user-defined functions (scalar, inline, andmultistatement
* User-defined functions are useful for both the performance enhancements they provide because of
their cached execution plans and their ability to encapsulate reusable code.

``` sql 

-----------------------------------------------------
-- Create Function
-----------------------------------------------------

IF OBJECT_ID (N'dbo.udf_CheckForSQLInjection', N'FN') IS NOT NULL
    DROP FUNCTION udf_CheckForSQLInjection;
GO

-----------------------------------------------------
-- Create Scalar functions
-----------------------------------------------------
CREATE FUNCTION dbo.udf_CheckForSQLInjection
(@TSQLString varchar(max))
RETURNS BIT
AS
BEGIN
	DECLARE @IsSuspect bit
	-- UDF assumes string will be left padded with a single space
	SET @TSQLString = ' ' + @TSQLString 
	IF (PATINDEX('% xp_%' , @TSQLString ) <> 0 OR PATINDEX('% OPENROWSET %' , @TSQLString )<> 0 
	BEGIN
		SELECT @IsSuspect = 1
	END
	ELSE
	BEGIN
		SELECT @IsSuspect = 0
	END

	RETURN (@IsSuspect)

END
GO

-----------------------------------------------------
-- Create Table Value functions
-----------------------------------------------------
CREATE FUNCTION dbo.ufn_SalesByStore 
(@storeid int)
RETURNS TABLE
AS
RETURN 
(
    SELECT * FROM Production.Product AS P 
);

-----------------------------------------------------
-- Create Multi-Statement User-Defined Functions
-----------------------------------------------------
CREATE FUNCTION dbo.ufn_FindReports (@InEmpID INTEGER)
RETURNS @retFindReports TABLE 
(
    EmployeeID int primary key NOT NULL,
    FirstName nvarchar(255) NOT NULL,
    JobTitle nvarchar(50) NOT NULL
)
--Returns a result set that lists all the employees who report to the 
--specific employee directly or indirectly.*/
AS
BEGIN
   SELECT EmployeeID, FirstName, LastName, JobTitle, RecursionLevel
   FROM EMP_cte 
   RETURN
END;
GO

-----------------------------------------------------
-- Use scalar User-DefinedFunction
-----------------------------------------------------
SELECT dbo.udf_ProperCase(DocumentSummary)

-----------------------------------------------------
-- Use Table Value functions or Inline User-Defined Functions
-----------------------------------------------------
SELECT * FROM Sales.ufn_SalesByStore (602);

-----------------------------------------------------
-- Use Multi-Statement User-Defined Functions
-----------------------------------------------------
SELECT EmployeeID, FirstName, JobTitle FROM dbo.ufn_FindReports(1); 

-----------------------------------------------------
-- Drop User-Defined Functions
-----------------------------------------------------
DROP FUNCTION dbo.udf_ParseArray

-----------------------------------------------------
-- Displaying the definition of Transact-SQL user-defined functions
-----------------------------------------------------
SELECT definition, type 
FROM sys.sql_modules AS m
JOIN sys.objects AS o ON m.object_id = o.object_id AND type IN ('FN', 'IF', 'TF');


``` 

## User Defined Types

``` sql 
CREATE TYPE dbo.AccountNBR FROM char(14) NOT NULL
GO

CREATE TABLE dbo.InventoryAccount
(InventoryAccountID int NOT NULL,
InventoryAccountNBR AccountNBR)
GO

DROP TYPE dbo.AccountNBR




``` 

## Triggers
``` sql 


-- Remove trigger if one already exists with same name
IF EXISTS (SELECT 1 FROM sys.triggers WHERE object_id = OBJECT_ID(N'[Production].[trg_uid_ProductInventoryAudit]'))
	DROP TRIGGER [Production].[trg_uid_ProductInventoryAudit]
GO


-- Create trigger to populate Production.ProductInventoryAudit table
CREATE TRIGGER Production.trg_uid_ProductInventoryAudit
ON Production.ProductInventory
AFTER INSERT, DELETE
AS
	SET NOCOUNT ON

	-- Inserted rows
	INSERT Production.ProductInventoryAudit
	(ProductID, LocationID, Shelf, Bin, Quantity,
	rowguid, ModifiedDate, InsOrUPD)
	SELECT DISTINCT i.ProductID, i.LocationID, i.Shelf, i.Bin, i.Quantity,
	i.rowguid, GETDATE(), 'I'
	FROM inserted i

	-- Deleted rows
	INSERT Production.ProductInventoryAudit
	(ProductID, LocationID, Shelf, Bin, Quantity,
	rowguid, ModifiedDate, InsOrUPD)
	SELECT d.ProductID, d.LocationID, d.Shelf, d.Bin, d.Quantity,
	d.rowguid, GETDATE(), 'D'
	FROM deleted d
	
	IF EXISTS 	(SELECT Shelf	FROM inserted	WHERE Shelf = 'A')
	BEGIN
		PRINT 'Shelf ''A'' is closed for new inventory.'
		ROLLBACK
	END
	
	IF UPDATE(GroupName)
	BEGIN
		PRINT 'Updates to GroupName require DBA involvement.'
		ROLLBACK
	END


GO

--Creating a DDL Trigger That Audits Database-Level Events
CREATE TRIGGER db_trg_RestrictINDEXChanges
ON DATABASE
FOR CREATE_INDEX, ALTER_INDEX, DROP_INDEX
AS
	SET NOCOUNT ON
	INSERT dbo.ChangeAttempt
	(EventData, DBUser)
	VALUES (EVENTDATA(), USER)
GO

--Creating a DDL Trigger That Audits Server-Level Events
-- Disallow new Logins on the SQL instance
CREATE TRIGGER srv_trg_RestrictNewLogins
ON ALL SERVER
FOR CREATE_LOGIN
AS
	PRINT 'No login creations without DBA involvement.'
	ROLLBACK
GO
--Next, an attempt ismade to add a new SQL login:
CREATE LOGIN JoeS WITH PASSWORD = 'A235921'
GO


DROP TRIGGER srv_trg_RestrictNewLogins ON ALL SERVER


----------------------------------------------
-- Viewing DML TriggerMetadata
----------------------------------------------

-- Show the DML triggers in the current database
SELECT OBJECT_NAME(parent_id) Table_or_ViewNM,
name TriggerNM,
is_instead_of_trigger,
is_disabled
FROM sys.triggers
WHERE parent_class_desc = 'OBJECT_OR_COLUMN'
ORDER BY OBJECT_NAME(parent_id), name


--To display a specific trigger’s Transact-SQL definition, you can query the sys.sql_modules systemcatalog view:

-- Displays the trigger SQL definition
--(if the trigger is not encrypted)
SELECT o.name, m.definition
FROM sys.sql_modules m
INNER JOIN sys.objects o ON
m.object_id = o.object_id
WHERE o.type = 'TR'

--Viewing DDL TriggerMetadata
-- Show the DML triggers in the current database
SELECT name TriggerNM, is_disabled
FROM sys.triggers
WHERE parent_class_desc = 'DATABASE'
ORDER BY OBJECT_NAME(parent_id), name

--Modifying a Trigger
ALTER TRIGGER srv_trg_RestrictNewLogins
ON ALL SERVER
FOR CREATE_LOGIN
AS
SET NOCOUNT ON
PRINT 'Your login creation is being monitored.'
INSERT AdventureWorks.dbo.ChangeAttempt
(EventData, DBUser)
VALUES (EVENTDATA(), USER)
GO

--the trigger is disable using the DISABLE TRIGGER command:
DISABLE TRIGGER HumanResources.trg_Department ON HumanResources.Department

--the trigger is enabled using the ENABLE TRIGGER command:
ENABLE TRIGGER HumanResources.trg_Department ON HumanResources.Department

--Limiting Trigger Nesting
-- Disable nesting
EXEC sp_configure 'nested triggers', 0
RECONFIGURE WITH OVERRIDE
GO
-- Enable nesting
EXEC sp_configure 'nested triggers', 1
RECONFIGURE WITH OVERRIDE
GO

--Controlling Trigger Recursion
-- Allows recursion
ALTER DATABASE AdventureWorks
SET RECURSIVE_TRIGGERS ON
-- View the db setting
SELECT is_recursive_triggers_on
FROM sys.databases
WHERE name = 'AdventureWorks'
-- Prevents recursion
ALTER DATABASE AdventureWorks
SET RECURSIVE_TRIGGERS OFF
-- View the db setting
SELECT is_recursive_triggers_on
FROM sys.databases
WHERE name = 'AdventureWorks'


--Setting Trigger Firing Order
EXEC sp_settriggerorder 'trg_i_TestTriggerOrder', 'First', 'INSERT'
EXEC sp_settriggerorder 'trg_i_TestTriggerOrder2', 'Last', 'INSERT'


-- Drop a DML trigger
DROP TRIGGER dbo.trg_i_TestTriggerOrder
-- Drop multiple DML triggers
DROP TRIGGER dbo.trg_i_TestTriggerOrder2, dbo.trg_i_TestTriggerOrder3
-- Drop a DDL trigger
DROP TRIGGER db_trg_RestrictINDEXChanges
ON DATABASE



``` 


## Error Handling
* Nesting Error Handling
* TRY...CATCH statements can be nested, which means you can use the TRY...CATCH statements within other TRY...CATCH blocks. 
* This allows you to handle errors that may happen, even in your error handling.


``` sql 

EXEC sp_addmessage
100001,
14,
N'The current table %s is not updateable by your group!'
GO
-- Using the new message (RAISERROR reviewed in the next recipe)
RAISERROR (100001, 14, 1, N'HumanResources.Employee')



--drops the user-defined error message
EXEC sp_dropmessage 100001

BEGIN TRY
	BEGIN TRAN

	INSERT Production.Location 	(Name, CostRate, Availability)
	VALUES 	('Tool Verification', 0.00, 0.00)
	
	COMMIT TRANSACTION
END TRY
BEGIN CATCH
	SELECT ERROR_NUMBER() ErrorNBR, ERROR_SEVERITY() Severity, ERROR_LINE () ErrorLine, ERROR_MESSAGE() Msg
	ROLLBACK TRANSACTION
END CATCH

``` 


## Manage Database Security

``` sql 

---------------------------------------------------------
-- LOGIN
---------------------------------------------------------

-- For Windows Authentication
--Creating a login from a Windows domain account
CREATE LOGIN 'domain\rams1' FROM WINDOWS;

-- For SQL Server Authentication

--Creating a SQL Server authentication login with a password
CREATE LOGIN Mary7 WITH PASSWORD = 'A2c3456$#' ;

--creates the login Mary8 with password some of the optional arguments.
CREATE LOGIN Mary8 WITH PASSWORD = 'A2c3456$#' MUST_CHANGE, DEFAULT_DATABASE = 'MyDB', DEFAULT_LANGUAGE='ENG', CHECK_EXPIRATION = ON, CHECK_POLICY = ON;

--Creating aWindows Login
CREATE LOGIN [CAESAR\Livia]
FROM WINDOWS
WITH DEFAULT_DATABASE = AdventureWorks,
DEFAULT_LANGUAGE = English

CREATE LOGIN Veronica
WITH PASSWORD = 'ChangeMe' MUST_CHANGE, CHECK_EXPIRATION = ON, CHECK_POLICY = ON
DEFAULT_DATABASE = AdventureWorks


--creates a login from a Windows domain account named Mary in the Contoso domain.
CREATE LOGIN [Contoso\Mary] FROM WINDOWS;

-- Get login information
SELECT name, sid FROM sys.sql_logins WHERE name = 'TestLogin';


--D. Creating a login from a certificate
CREATE CERTIFICATE certificateName
    WITH SUBJECT = '<login_name> certificate in master database',
    EXPIRY_DATE = '12/05/2025';
GO
CREATE LOGIN Mary8 FROM CERTIFICATEcertificateName  

ALTER LOGIN Mary8 WITH PASSWORD = 'A2c3456$#' ;


ALTER LOGIN Veronica
WITH PASSWORD = 'InfernoIII'
OLD_PASSWORD = 'InfernoII'


ALTER LOGIN Mary8 WITH NAME = 'Rams' 

ALTER LOGIN Mary8 DISABLE;

--Dropping a SQL Login
DROP LOGIN Mary8

-- Windows Group login
DROP LOGIN [CAESAR\Senators]

-- Windows user login
DROP LOGIN [CAESAR\Livia]


SELECT name, sid
FROM sys.server_principals
WHERE type_desc IN ('SQL_LOGIN')
ORDER BY name


SELECT name, sid
FROM sys.server_principals
WHERE type_desc IN ('WINDOWS_LOGIN', 'WINDOWS_GROUP')
ORDER BY type_desc


---------------------------------------------------------
-- USER
-- Database Principals
---------------------------------------------------------

--Users based on logins in master
CREATE USER [Domain1\WindowsUserBarry]
CREATE USER [Domain1\WindowsUserBarry] FOR LOGIN Domain1\WindowsUserBarry
CREATE USER [Domain1\WindowsUserBarry] FROM LOGIN Domain1\WindowsUserBarry
CREATE USER [Domain1\WindowsGroupManagers]
CREATE USER [Domain1\WindowsGroupManagers] FOR LOGIN [Domain1\WindowsGroupManagers]
CREATE USER [Domain1\WindowsGroupManagers] FROM LOGIN [Domain1\WindowsGroupManagers]
CREATE USER SQLAUTHLOGIN
CREATE USER SQLAUTHLOGIN FOR LOGIN SQLAUTHLOGIN
CREATE USER SQLAUTHLOGIN FROM LOGIN SQLAUTHLOGIN

--Users that authenticate at the database
CREATE USER [Domain1\WindowsUserBarry]
CREATE USER [Domain1\WindowsGroupManagers]
CREATE USER Barry WITH PASSWORD = 'sdjklalie8rew8337!$d'

--Users based on Windows principals without logins in master
CREATE USER [Domain1\WindowsUserBarry]
CREATE USER [Domain1\WindowsUserBarry] FOR LOGIN Domain1\WindowsUserBarry
CREATE USER [Domain1\WindowsUserBarry] FROM LOGIN Domain1\WindowsUserBarry
CREATE USER [Domain1\WindowsGroupManagers]
CREATE USER [Domain1\WindowsGroupManagers] FOR LOGIN [Domain1\WindowsGroupManagers]
CREATE USER [Domain1\WindowsGroupManagers] FROM LOGIN [Domain1\WindowsGroupManagers]

--Users that cannot authenticate
CREATE USER RIGHTSHOLDER WITHOUT LOGIN
CREATE USER CERTUSER FOR CERTIFICATE SpecialCert
CREATE USER CERTUSER FROM CERTIFICATE SpecialCert
CREATE USER KEYUSER FOR ASYMMETRIC KEY SecureKey
CREATE USER KEYUSER FROM ASYMMETRIC KEY SecureKey


--Creating a database user based on a SQL Server login
CREATE USER AbolrousHazem FOR LOGIN AbolrousHazem;  

--Creating a database user with a default schema
CREATE USER Wanida FOR LOGIN WanidaBenshoof WITH DEFAULT_SCHEMA = Marketing;  

--Creating and using a user without a login
CREATE USER CustomApp WITHOUT LOGIN ;  
GRANT IMPERSONATE ON USER::CustomApp TO [adventure-works\tengiz0] ;  

CREATE USER Carlo  
WITH PASSWORD='RN92piTCh%$!~3K9844 Bl*'  
    , DEFAULT_LANGUAGE=[Brazilian]  
    , DEFAULT_SCHEMA=[dbo]  
    
    
--Creating a contained database user for a domain login
CREATE USER [Contoso\Fritz] ; 

--Creating a contained database user with a specific SID
CREATE USER CarmenW WITH PASSWORD = 'a8ea v*(Rd##+', SID = 0x01050000000000090300000063FF0451A9E7664BA705B10E37DDC4B7;  

--Creating a user to copy encrypted data
CREATE USER [Chin] WITH  DEFAULT_SCHEMA = dbo, ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = ON ;      


CREATE USER Veronica

ALTER USER Veronica WITH NAME = VSanders

DROP USER VSanders


ALTER USER Sonja
WITH LOGIN = Sonja


DROP USER CarmenW

---------------------------------------------------------
-- SCHEMA
---------------------------------------------------------


--Creating a schema and granting permissions
CREATE SCHEMA Sales AUTHORIZATION Annik
    CREATE TABLE NineProngs (source int, cost int, partnumber int)
    GRANT SELECT ON SCHEMA::Sales TO Mandar
    DENY SELECT ON SCHEMA::Sales TO Prasanna;
    

CREATE TABLE Sales.Region 
(Region_id int NOT NULL,
Region_Name char(5) NOT NULL)
WITH (DISTRIBUTION = REPLICATE);
GO

-- creates a schema Production owned by Mary.
CREATE SCHEMA Sales AUTHORIZATION [Contoso\Mary];

--Transferring a table from one schema to another
ALTER SCHEMA HumanResources TRANSFER Person.Address;

DROP SCHEMA Sales

---------------------------------------------------------
-- GRANT
---------------------------------------------------------


--Granting EXECUTE permission on a stored procedure
GRANT EXECUTE ON TestProc TO TesterRole WITH GRANT OPTION;
GRANT CREATE TABLE TO MelanieK;
GRANT SHOWPLAN TO AuditMonitor;
GRANT CREATE VIEW TO CarmineEs WITH GRANT OPTION;

--Granting SELECT permission on a table
GRANT SELECT ON OBJECT::Person.Address TO RosaQdM;

--Granting REFERENCES permission on a view with GRANT OPTION
GRANT REFERENCES (BusinessEntityID) ON OBJECT::HumanResources.vEmployee      TO Wanida WITH GRANT OPTION;

--Granting SELECT permission on a table to a domain account
GRANT SELECT ON Person.Address TO RosaQdM;

--Granting SELECT permission on a table to a domain account
GRANT SELECT ON Person.Address TO [AdventureWorks2012\RosaQdM];

--Granting EXECUTE permission on a procedure to a role
GRANT EXECUTE ON dbo.uspGetBillOfMaterials TO newrole ;

--Granting IMPERSONATE permission on a login
GRANT IMPERSONATE ON LOGIN::WanidaBenshoof to [AdvWorks\YoonM];

--Granting VIEW DEFINITION permission with GRANT OPTION
GRANT VIEW DEFINITION ON LOGIN::EricKurjan TO RMeyyappan WITH GRANT OPTION;

--Granting VIEW DEFINITION permission on a server role
GRANT VIEW DEFINITION ON SERVER ROLE::Sales TO Auditors ;

Grant SELECT Oermision to specific columns
GRANT SELECT ON Person.Address (Name, Age, Adderessm Zipcode)

GRANT ALTER ON Vendors TO Susan

GRANT INSERT, UPDATE, DELETE
ON Invoices
TO  Susan

GRANT SELECT ON Sales.vSalesPersonSalesByFiscalYears
TO DataWareHouseApp


GRANT CONNECT SQL TO [CAESAR\Helen]

GRANT SELECT ON HumanResources.Employee TO HR_ReportSpecialist



---------------------------------------------------------
-- REVOKE
---------------------------------------------------------

REVOKE DELETE
ON Invoices
FROM Susan

--Revoking SELECT permission on a table
REVOKE SELECT ON OBJECT::Person.Address FROM RosaQdM;

--Revoking EXECUTE permission on a stored procedure
REVOKE EXECUTE ON OBJECT::HumanResources.uspUpdateEmployeeHireInfo
    FROM Recruiting11;
    
--Revoking REFERENCES permission on a view with CASCADE    
REVOKE REFERENCES (BusinessEntityID) ON OBJECT::HumanResources.vEmployee 
    FROM Wanida CASCADE;

--Revoke Privileges on Table    
REVOKE privileges ON object FROM user;    

REVOKE DELETE ON employees FROM anderson;

REVOKE ALL ON employees FROM anderson;

REVOKE SELECT ON employees FROM public;


---------------------------------------------------------
-- Server Role
---------------------------------------------------------

-- Assign a user to a server role
ALTER SERVER ROLE Sysadmin ADD MEMBER Rams

-- Remove a user to a server role
ALTER SERVER ROLE Sysadmin DROP MEMBER Rams

-- create a new server role
CREATE SERVER ROLE buyers

--Creating a server role that is owned by a login
CREATE SERVER ROLE buyers AUTHORIZATION BenMiller;

--Creating a server role that is owned by a fixed server role
CREATE SERVER ROLE auditors AUTHORIZATION securityadmin;

DROP SERVER ROLE auditors


ALTER ROLE HR_ReportSpecialist WITH NAME = HumanResources_RS


CREATE ROLE role_name [ AUTHORIZATION owner_name ]

ALTER ROLE role_name WITH NAME = new_name

DROP ROLE HumanResources_RS


---------------------------------------------------------
-- Application Role
---------------------------------------------------------

CREATE APPLICATION ROLE DataWareHouseApp
WITH PASSWORD = 'mywarehouse123!',
DEFAULT_SCHEMA = dbo



---------------------------------------------------------
-- Deny
---------------------------------------------------------
DENY CONNECT SQL TO [CAESAR\Helen]


---------------------------------------------------------
-- Deny
---------------------------------------------------------


EXEC master..sp_addsrvrolemember 'Veronica', 'sysadmin'
GO

EXEC master..sp_dropsrvrolemember 'Veronica', 'sysadmin'
GO

SELECT name
FROM sys.server_principals
WHERE type_desc = 'SERVER_ROLE'


EXEC sp_addrolemember 'HR_ReportSpecialist', 'Veronica'
EXEC sp_addrolemember 'db_datawriter', 'Helen'

EXEC sp_droprolemember 'db_datawriter', 'Helen'

EXEC sp_helprole



``` 

## Database 

``` sql 

IF  EXISTS (SELECT name FROM sys.databases WHERE name = 'BookStore')
	DROP DATABASE BookStore
GO

USE BookStore
GO

--Viewing Database Information
EXEC sp_helpdb 'BookStore'
GO


ALTER DATABASE AdventureWorks
SET COMPATIBILITY_LEVEL = 100
GO




CREATE DATABASE BookStoreArchive
ON PRIMARY
	--Every database has one primary data file that keeps track of all the rest of the files in the database, in addition to storing data. 
	-- By convention, a primary data file has the extension .mdf.
	--Primary data files
	( NAME = 'BookStoreArchive',
	FILENAME = 'F:\Apress\BookStoreArchive.mdf' ,
	SIZE = 3MB ,
	MAXSIZE = UNLIMITED,
	FILEGROWTH = 10MB ),

	--Secondary data files
	--A database can have zero or more secondary data files. 
	--By convention, a secondary data file has the extension .ndf.
	( NAME = 'BookStoreArchive2',
	FILENAME = 'G:\Apress\BookStoreArchive2.ndf' ,
	SIZE = 1MB ,
	MAXSIZE = 30,
	FILEGROWTH = 5% ),
	
	--Secondary data files in diffrent filegroup
	FILEGROUP SalesGroup1
	( NAME = salesGrp1Fi1e1,
	FILENAME =
	'C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\DATA\salesGrp1Fi1e1.ndf',
	SIZE = 500, MAXSIZE = 3000,
	FILEGROWTH = 500 ),

	--Filestream filegroups (Filestream.hdr)
	FILEGROUP MovieReviewsFSGroup1 CONTAINS FILESTREAM
	( NAME = Reviews_FS,
	FILENAME = 'c:\data\Reviews_FS')

	--Log files
	--Every database has at least one log file that contains the information necessary to recover all transactions in a database. 
	--By convention, a log file has the extension .ldf.
	LOG ON
	( NAME = 'BookStoreArchive_log',
	FILENAME = 'H:\Apress\BookStoreArchive_log.LDF' ,
	SIZE = 504KB ,
	MAXSIZE = 100MB ,
	FILEGROWTH = 10%)
GO


--SINGLE_USER | RESTRICTETED_USER | MULTI_USER
ALTER DATABASE AdventureWorks SET SINGLE_USER;

--This query returns MULTI_USER, SINGLE_USER, or RESTRICTED_USER.
SELECT USER_ACCESS_DESC FROM sys.databases WHERE name = '<name of database>';

--OFFLINE | ONLINE | EMERGENCY
ALTER DATABASE AdventureWorks SET OFFLINE;


SELECT state_desc from sys.databases WHERE name = 'AdventureWorks';

--REAEAD_ONLY | REAEAD_WRITETE
ALTER DATABASE AdventureWorks SET READ_ONLY;
 
SELECT name, is_read_only FROM sys.databases WHERE name = 'AdventureWorks';


--Database security
SELECT s.name as [Login Name], d.name as [User Name],
default_schema_name as [Default Schema]
FROM sys.database_principals d
LEFT JOIN sys.server_principals s
ON s.sid = d.sid
WHERE d.type_description = 'SQL_USER';


--Detaching and reattaching a database
EXEC sp_detach_db <name of database>;

--Understanding compatibility levels
SELECT compatibility_level FROM sys.databases WHERE name = '<database name>';

ALTER DATABASE <database name> SET COMPATIBILITY_LEVEL = <compatibility-level>;



SELECT user_access_desc
FROM sys.databases
WHERE name = 'AdventureWorks'

ALTER DATABASE AdventureWorks
SET SINGLE_USER
WITH ROLLBACK IMMEDIATE
SELECT user_access_desc
FROM sys.databases
WHERE name = 'AdventureWorks'
ALTER DATABASE AdventureWorks
SET MULTI_USER
SELECT user_access_desc
FROM sys.databases
WHERE name = 'AdventureWorks'

--Renaming a Database
ALTER DATABASE BookWarehouse SET SINGLE_USER WITH ROLLBACK IMMEDIATE
GO

ALTER DATABASE BookWarehouse MODIFY NAME = BookMart
GO

ALTER DATABASE BookMart SET MULTI_USER
GO

--Dropping a Database
ALTER DATABASE BookStoreArchive_Ukrainian
SET SINGLE_USER
WITH ROLLBACK IMMEDIATE
GO

DROP DATABASE BookStoreArchive_Ukrainian
GO

--Detaching a Database
ALTER DATABASE TestDetach
SET SINGLE_USER
WITH ROLLBACK IMMEDIATE

EXEC sp_detach_db 'TestDetach', 'false' -- don't skip checks

--Viewing Database Options
SELECT name, is_read_only, is_auto_close_on, is_auto_shrink_on
FROM sys.databases
WHERE name = 'AdventureWorks'

SELECT is_ansi_nulls_on
FROM sys.databases
WHERE name = 'AdventureWorks'

ALTER DATABASE AdventureWorks
SET ANSI_NULLS OFF

--Changing a Database State to Online,Offline, or Emergency
ALTER DATABASE AdventureWorks SET OFFLINE	--{ ONLINE | OFFLINE | EMERGENCY }


SELECT name
FROM sys.database_files

DBCC SHRINKFILE(BookData2, EMPTYFILE)

ALTER DATABASE BookData REMOVE FILE BookData2


--Relocating a Data or Transaction Log File
ALTER DATABASE BookTransferHouse
MODIFY FILE
(NAME = 'BookTransferHouse', FILENAME = 'C:\Apress\BookTransferHouse.mdf')
GO

--Increasing a Database’s File Size andModifying Its Growth Options
ALTER DATABASE BookTransferHouse
MODIFY FILE
(NAME='BookTransferHouse_DataFile1', SIZE=6MB, MAXSIZE=10MB)


--Removing a Filegroup


--Making a Database or Filegroup Read-Only
-- Make the database read only
ALTER DATABASE BookTransferHouse
SET READ_ONLY
GO
-- Allow updates again
ALTER DATABASE BookTransferHouse
SET READ_WRITE
GO

-- Add a new filegroup
ALTER DATABASE BookTransferHouse
ADD FILEGROUP FG4
GO
-- Add a file to the filegroup
ALTER DATABASE BookTransferHouse
ADD FILE
( NAME = 'BW4',
FILENAME = 'C:\Apress\BW4.NDF' ,
SIZE = 1MB ,
MAXSIZE = 50MB,
FILEGROWTH = 5MB )
TO FILEGROUP [FG4]
GO
-- Make a specific filegroup read-only
ALTER DATABASE BookTransferHouse
MODIFY FILEGROUP FG4 READ_ONLY
GO
-- Allow updates again
ALTER DATABASE BookTransferHouse
MODIFY FILEGROUP FG4 READ_WRITE
GO

--Viewing and Managing Database Space Usage
EXEC sp_spaceused
DBCC SQLPERF ( LOGSPACE )

--Shrinking the Database or a Database File
DBCC SHRINKDATABASE ('AdventureWorks', 10)

DBCC SHRINKFILE ('AdventureWorks_Log', 100)

ALTER DATABASE AdventureWorks
MODIFY FILE (NAME = AdventureWorks2008_Data , SIZE= 250MB)
GO
ALTER DATABASE AdventureWorks
MODIFY FILE (NAME = AdventureWorks2008_Log , SIZE= 500MB)
GO

``` 


## Sample

``` sql 

--Viewing Database Information
EXEC sp_helpdb 'BookStore'
GO

IF NOT EXISTS (SELECT name
FROM sys.databases
WHERE name = 'BookStore')


CREATE DATABASE database_name


Viewing Database Information
EXEC sp_helpdb 'BookStore'

ALTER DATABASE AdventureWorks
SET SINGLE_USER
WITH ROLLBACK IMMEDIATE
SET MULTI_USER
MODIFY NAME = BookMart


DROP DATABASE BookStoreArchive_Ukrainian


EXEC sp_detach_db 'TestDetach', 'false' -- don't skip checks


DBCC CHECKALLOC ('AdventureWorks')
DBCC CHECKFILEGROUP('PRIMARY')
DBCC CHECKTABLE ('Production.Product') WITH ALL_ERRORMSGS
DBCC CHECKTABLE ('Sales.SalesOrderDetail') WITH ESTIMATEONLY
DBCC CHECKTABLE ('Sales.SalesOrderDetail', 3) WITH PHYSICAL_ONLY
DBCC CHECKCATALOG ('AdventureWorks')


-- Rename the table
EXEC sys.sp_rename 'HumanResources.InsuranceProvider', 'Provider', 'Object'

-- Rename a column
EXEC sys.sp_rename 'HumanResources.Provider.InsuranceProviderID', 'ProviderID', 'Column'

-- Rename the primary key constraint
EXEC sys.sp_rename 'HumanResources.Provider.ni_InsuranceProvider_InsuranceProviderID', 'ni_Provider_ProviderID', 'Index'



ALTER SCHEMA schema_name TRANSFER object_name


``` 

## Sample

``` sql 



-- To use named parameters:
EXEC sp_addlinkedserver 
   @server = 'DBSERVER', 
   @provider = 'MSQLNCLI', 
   @datasrc = 'localhost\sqlExpress'



-- To use named parameters:
EXEC sp_addlinkedserver 
   @server = 'SEATTLE Mktg', 
   @provider = 'Microsoft.Jet.OLEDB.4.0', 
   @srvproduct = 'OLE DB Provider for Jet',
   @datasrc = 'C:\MSOffice\Access\Samples\Northwind.mdb'


-- To use named parameters:
EXEC sp_addlinkedserver
   @server = 'LONDON Mktg',
   @srvproduct = 'Oracle',
   @provider = 'MSDAORA',
   @datasrc = 'MyServer'
GO


-- To use named parameters:
EXEC sp_addlinkedserver 
   @server = 'LONDON Payroll', 
   @srvproduct = '',
   @provider = 'MSDASQL',
   @provstr = 'DRIVER={SQL Server};SERVER=MyServer;UID=sa;PWD=sapassword;'



EXEC sp_addlinkedserver 'ExcelSource',
   'Jet 4.0',
   'Microsoft.Jet.OLEDB.4.0',
   'c:\MyData\DistExcl.xls',
   NULL,
   'Excel 5.0'
GO

``` 

## Sample

``` sql 
USE master;
EXEC sp_configure 'show advanced option', 1;
RECONFIGURE;
exec sp_configure 'min server memory (MB)', 5120;
exec sp_configure 'max server memory (MB)', 10240;
RECONFIGURE WITH OVERRIDE;

``` 




## Work XML

``` sql 
-------------------------------------------------
-- Sample 1
-------------------------------------------------
DECLARE @xmlCar xml;
DECLARE @strCar varchar(max);
SET @xmlCar =
'<Car id="1234">
  <Make>Volkswagen</Make>
  <Model>Eurovan</Model>
  <Year>2003</Year>
  <Color>White</Color>
</Car>'
SET @strCar = CAST(@xmlCar AS varchar(max));
SELECT @strCar;

-------------------------------------------------
-- Sample 2
-------------------------------------------------
SELECT FirstName, Lastname 
    FROM Person.Person
    FOR XML PATH

-------------------------------------------------
-- Sample 3
-------------------------------------------------
SELECT FirstName, Lastname 
 FROM Person.Person
 FOR XML PATH ('Employee'), Elements, ROOT ('Employees')
     
-------------------------------------------------
-- Sample 4
-------------------------------------------------
SELECT Cust.CustomerID, 
       OrderHeader.CustomerID,
       OrderHeader.SalesOrderID, 
       OrderHeader.Status,
       Cust.CustomerType
FROM Sales.Customer Cust, Sales.SalesOrderHeader OrderHeader
WHERE Cust.CustomerID = OrderHeader.CustomerID
ORDER BY Cust.CustomerID
FOR XML AUTO, ELEMENTS



```


## Work with Blobs 

``` sql 

```

## Work with Blobs 

``` sql 

```


## More store procedure

``` sql 
--The remote stored procedure may be executed by means of the four-part name:
EXECUTE Server.Database.Schema.StoredProcedureName;

--Alternatively, you can use the OpenQuery() function to call a remote stored procedure:
OpenQuery(LinkedServerName, 'EXECUTE Schema.StoredProcedureName');


--Providing Lists and Tables as Input Parameters to Stored Procedures
--Providing a List as an Input Parameter
CREATE PROCEDURE Sales.uspGetCurrencyRate
@CurrencyRateIDList varchar(50)
AS
DECLARE @SQLString nvarchar(1000)
SET @SQLString = N'
SELECT CurrencyRateID, CurrencyRateDate, FromCurrencyCode,
ToCurrencyCode, AverageRate, EndOfDayRate
FROM Sales.CurrencyRate
WHERE CurrencyRateID in ('+@CurrencyRateIDList+');'
EXECUTE sp_executesql @SQLString;
GO
EXECUTE Sales.uspGetCurrencyRate @CurrencyRateIDList = '1, 4, 6, 7';


--Providing a Table as an Input Parameter
CREATE PROCEDURE Sales.uspGetCurrencyRatesXML
@XMLList varchar(1000)
,@CurrencyRateDate datetime
AS
DECLARE @XMLDocHandle int
DECLARE @CurrencyCodeTable table
(
FromCurrencyCode char(3)
,ToCurrencyCode char(3)
)
EXECUTE sp_xml_preparedocument @XMLDocHandle OUTPUT, @XMLlist;
INSERT INTO @CurrencyCodeTable(FromCurrencyCode, ToCurrencyCode)
SELECT FromCurrencyCode, ToCurrencyCode
FROM OPENXML (@XMLDocHandle, '/ROOT/CurrencyList',1)
WITH (
FromCurrencyCode char(3)
,ToCurrencyCode char(3)
);
SELECT cr.CurrencyRateID, cr.FromCurrencyCode,
cr.ToCurrencyCode, cr.AverageRate,
cr.EndOfDayRate, cr.CurrencyRateDate
FROM Sales.CurrencyRate cr
JOIN @CurrencyCodeTable tvp
ON cr.FromCurrencyCode = tvp.FromCurrencyCode
AND cr.ToCurrencyCode = tvp.ToCurrencyCode
WHERE CurrencyRateDate = @CurrencyRateDate;
EXECUTE sp_xml_removedocument @XMLDocHandle;
GO

--Execute the stored procedure
EXECUTE Sales.uspGetCurrencyRatesXML @XMLList ='
<ROOT>
<CurrencyList FromCurrencyCode="USD" ToCurrencyCode="AUD"> </CurrencyList>
<CurrencyList FromCurrencyCode="USD" ToCurrencyCode="EUR"> </CurrencyList>
<CurrencyList FromCurrencyCode="USD" ToCurrencyCode="GBP"> </CurrencyList>
<CurrencyList FromCurrencyCode="USD" ToCurrencyCode="MXN"> </CurrencyList>
</ROOT>', @CurrencyRateDate = '2005-07-14';



--Providing a Table as an Input Parameter
CREATE PROCEDURE Sales.uspGetCurrencyRatesXML
@XMLList varchar(1000)
,@CurrencyRateDate datetime
AS
DECLARE @XMLDocHandle int
DECLARE @CurrencyCodeTable table
(
FromCurrencyCode char(3)
,ToCurrencyCode char(3)
)
EXECUTE sp_xml_preparedocument @XMLDocHandle OUTPUT, @XMLlist;
INSERT INTO @CurrencyCodeTable(FromCurrencyCode, ToCurrencyCode)
SELECT FromCurrencyCode, ToCurrencyCode
FROM OPENXML (@XMLDocHandle, '/ROOT/CurrencyList',1)
WITH (
FromCurrencyCode char(3)
,ToCurrencyCode char(3)
);
SELECT cr.CurrencyRateID, cr.FromCurrencyCode,
cr.ToCurrencyCode, cr.AverageRate,
cr.EndOfDayRate, cr.CurrencyRateDate
FROM Sales.CurrencyRate cr
JOIN @CurrencyCodeTable tvp
ON cr.FromCurrencyCode = tvp.FromCurrencyCode
AND cr.ToCurrencyCode = tvp.ToCurrencyCode
WHERE CurrencyRateDate = @CurrencyRateDate;

EXECUTE sp_xml_removedocument @XMLDocHandle;
GO
--Execute the stored procedure
EXECUTE Sales.uspGetCurrencyRatesXML @XMLList ='
<ROOT>
<CurrencyList FromCurrencyCode="USD" ToCurrencyCode="AUD"> </CurrencyList>
<CurrencyList FromCurrencyCode="USD" ToCurrencyCode="EUR"> </CurrencyList>
<CurrencyList FromCurrencyCode="USD" ToCurrencyCode="GBP"> </CurrencyList>
<CurrencyList FromCurrencyCode="USD" ToCurrencyCode="MXN"> </CurrencyList>
</ROOT>', @CurrencyRateDate = '2005-07-14';






CREATE PROCEDURE Sales.uspGetCurrencyRatesUDT
@CurrencyCodeTable as CurrencyCodeListType READONLY
,@CurrencyRateDate date
AS
SELECT cr.CurrencyRateID, cr.FromCurrencyCode,
cr.ToCurrencyCode, cr.AverageRate,
cr.EndOfDayRate, cr.CurrencyRateDate
FROM Sales.CurrencyRate cr
JOIN @CurrencyCodeTable tvp
ON cr.FromCurrencyCode = tvp.FromCurrencyCode
AND cr.ToCurrencyCode = tvp.ToCurrencyCode
WHERE CurrencyRateDate = @CurrencyRateDate;
GO


DECLARE @CurrencyCodeTVP as CurrencyCodeListType
INSERT INTO @CurrencyCodeTVP(FromCurrencyCode, ToCurrencyCode)
VALUES
('USD', 'AUD'),
('USD', 'GBP'),
('USD', 'CAD'),
('USD', 'MXN');
EXECUTE Sales.uspGetCurrencyRatesUDT
@CurrencyCodeTable = @CurrencyCodeTVP,
@CurrencyRateDate = '2005-07-14';

```


## Configuration

``` sql 

SELECT DATABASEPROPERTYEX('CollateChange','Collation') AS DatabaseCollation;


SELECT
---Returns the name of the current user as he or she is known to the database.
USER_NAME() AS 'User',
--Returns the login name by which the user was authenticated to SQL Server.
SUSER_SNAME() AS 'Login',
--Returns the name of the user’s workstation.
HOST_NAME() AS 'Workstation',
--Returns the name of the application
APP_NAME() AS 'Application';



--Configuration
select @@VERSION


SELECT
SERVERPROPERTY('ProductVersion') AS ProductVersion,
SERVERPROPERTY('ProductLevel') AS ProductLevel,
SERVERPROPERTY('Edition') AS Edition;

--this procedure reports the current settings, as in the following code
EXEC sp_configure;

--Another method to display the advanced options is to turn on the show advanced options confi guration using the following code:
EXEC sp_configure 'show advanced options', 1;
RECONFIGURE

--The extended stored procedure, xp_msver, reports additional server and environment
EXEC xp_msver;

--The following example returns all the database properties of the AdventureWorks database:
SELECT * FROM sys.databases WHERE name = 'AdventureWorks';

--Connection properties can also be checked by means of the SessionProperty() function:
Select SESSIONPROPERTY ('ANSI_NULLS');

--Displaying the Advanced Options


SELECT name, minimum, maximum, value, value_in_use
FROM sys.configurations
WHERE is_advanced = 1
ORDER BY name;
The preceding example displays



--Startup Stored Procedures

EXEC sp_procoption @ProcName = 'ExistingSP',
@OptionName = 'startup',
@OptionValue = 'on'; -- on/off

--Use the following code to skip automatic execution for all startup stored procedures
EXEC sp_configure 'scan for startup procs', 0;
RECONFIGURE;



--The following code sets the min-memory confi guration to 1GB:
EXEC sp_configure 'min server memory', 1024;
RECONFIGURE;

--The following code sets the max-memory confi guration to 4GB
EXEC sp_configure 'max server memory', 4096;
RECONFIGURE;

--Minimum Query Memory
--The following code increases the minimum query memory to 2MB:
EXEC sp_configure 'min memory per query', 2048;
RECONFIGURE;


--Query Wait
--The following code specifi es that every query either starts executing within 20 seconds or times out.
EXEC sp_configure 'query wait', 20;
RECONFIGURE;

--Index Create Memory
--For example, the following code sets the memory used to create an index to 8MB:
EXEC sp_configure 'index create memory', 8096;
RECONFIGURE;


EXEC sp_configure 'affinity mask', 15;
RECONFIGURE;
EXEC sp_configure 'affinity I/O mask', 48;
RECONFIGURE;


EXEC sp_configure 'max worker threads', 128;
RECONFIGURE;

EXEC sp_configure 'max degree of parallelism', 4;
RECONFIGURE;

EXEC sp_configure 'c2 audit mode', 1;
RECONFIGURE;

EXEC sp_configure 'common criteria compliance enabled', 1;
RECONFIGURE;


--sets the maximum number of user connections to 10240
EXEC sp_configure 'user connections', 10240;
RECONFIGURE;

SELECT @@MAX_CONNECTIONS;

EXEC sp_configure 'query governor cost limit', 300;
RECONFIGURE;

EXEC sp_configure 'remote access', 0;
RECONFIGURE;

--Remote Login Timeout
EXEC sp_configure 'remote login timeout', 30;
RECONFIGURE;

--Remote Query Timeout
EXEC sp_configure 'remote query timeout', 600;
RECONFIGURE;

--Enforce DTC
EXEC sp_configure 'remote proc trans', 1;
RECONFIGURE;

--The following code sets the network-packet size to 2KB:
EXEC sp_configure 'network packet size', 2048;
RECONFIGURE;

```

## Backup & Recovery

``` sql 

--Backing Up the Database with Code
BACKUP DATABASE AdventureWorks2012
TO DISK = 'e:\AdventureWorks2012Backup.bak'
WITH NAME = 'AdventureWorks2012Backup';

--Backing Up the Database with Code - DIFFERENTIAL
BACKUP DATABASE AdventureWorks2012
TO DISK = 'e:\AdventureWorks2012Backup.bak'
WITH
DIFFERENTIAL,
NAME = 'AdventureWorks2012Backup';

--Verifying the Backup with Code
RESTORE VERIFYONLY
FROM DISK = 'e:\AdventureWorks2012Backup.bak'

--Backing Up the Transaction Log
BACKUP LOG AdventureWorks2012
TO DISK = 'e:\AdventureWorks2012Backup.bak'
WITH
NAME = 'AdventureWorks2012Backup';


RESTORE DATABASE Plan2Recover
FROM DISK = 'e:\P2R.bak'
With FILE = 1, NORECOVERY;

```


## Maintaining the Database 

``` sql 

--Database Integrity
DBCC CHECKDB ('AdventureWorks2012');


--Repairing the Database
ALTER DATABASE AdventureWorks2012 SET SINGLE_USER
WITH ROLLBACK IMMEDIATE;
BEGIN TRANSACTION;
DBCC CheckDB ('AdventureWorks2012', REPAIR_ALLOW_DATA_LOSS);
--Check for any data loss
--ROLLBACK TRANSACTION if data
--loss is not acceptable else COMMIT TRANSACTION;
ALTER DATABASE AdventureWorks2012 SET MULTI_USER;

--Object-Level Validation
DBCC CHECKALLOC ('database')
DBCC CHECKFILEGROUP ('filegroup')
DBCC CHECKTABLE('table')
DBCC CLEANTABLE ('database', "table")

--Data Integrity
DBCC CHECKCATALOG ('database'):
DBCC CHECKCONSTRAINTS ('table','constraint')
DBCC CHECKIDENT ('table')


DBCC CHECKIDENT ("HumanResources.Employee");
DBCC SQLPERF (LOGSPACE);
DBCC SHRINKDATABASE ('AdventureWorks2012', 10);

DBCC UPDATEUSAGE (AdventureWorks2012);
EXEC sp_spaceused;

DBCC SHRINKDATABASE ('AdventureWorks2012', 10);


DBCC OPENTRAN;

```

## Snapshot

``` sql 
--Creating a Database Snapshot
CREATE DATABASE AdventureWorks2012_Snapshot ON
(NAME = AdventureWorks2012_Data, FILENAME =
'D:\DATABASE SNAPSHOTS\AdventureWorks2012_Snapshot.snap' )
AS SNAPSHOT OF AdventureWorks2012;


--Querying Your Database Snapshots
USE AdventureWorks2012_Snapshot;
GO
SELECT Name, ProductNumber, ListPrice FROM Production.Product ORDER BY Name ASC;
GO

--Dropping a Database Snapshot
DROP DATABASE AdventureWorks2012_Snapshot;

--Rolling Back a Database Snapshot
RESTORE DATABASE AdventureWorks2012
FROM DATABASE_SNAPSHOT = 'AdventureWorks2012_Snapshot';

--Alternatively, you can also find the size using the dynamic management view sys.dm_io_virtual_file_stats as shown here:
SELECT size_on_disk_bytes FROM sys.dm_io_virtual_file_stats(DB_ID(N'AdventureWorks2012_Snapshot'),1);

```


## Manage Transcation and Locking

``` sql 

```




## System Stored Procedures

``` sql 
sp_help 'sp_dbobjectname'
sp_helptext 'sp_dbobjectname'
sp_helpdb 'dbname'
sp_who 'loginid'
sp_columns 'tablename'
```



## Others SQL

``` sql 
SELECT name, database_id, suser_sname(owner_sid) as owner,
create_date, user_access_desc, state_desc
FROM sys.databases
WHERE database_id <= 4;


--You can see FROM code dependencies using the function sys.dm_sql_referencing_
--entities(). For example, the following query would indicate whether any other SQL
--Server object referenced vEmployeeList:
SELECT *
FROM sys.dm_sql_referencing_entities
('dbo.vEmployeeList', 'Object')




The following query reports the current server collation:
SELECT SERVERPROPERTY('Collation') AS ServerCollation;

ALTER DATABASE CollateChange COLLATE SQL_Latin1_General_CP1_CS_AS;
GO




--WITH TIES Option
SELECT TOP(6) WITH TIES
ProductNumber, Name, ListPrice,
CONVERT(VARCHAR(10),SellStartDate,1) SellStartDate
FROM Production.Product
ORDER BY ListPrice DESC

--Selecting a Random Row
SELECT TOP(1) LastName
FROM Person.Person TableSample (10 Percent)
ORDER BY NewID();


-- NULL
SELECT 1 + NULL; -- Result: NULL


--User Information Functions

```

