### IMPLEMENTING A DATA-DRIVEN DECISION SYSTEM PART 1

**Introduction**
 
 As more organization begin to look for ways to maximise their business' potential, improve operations and return on Investments, they begin by seeking ways to integrate data-driven decision making into daily operations to uncover insights, there's the initial confusion and exasperation regarding the starting point. A a standard practice, most businesses have data repositories in form of ERP (Enterprise Resource Planning) systems, Relational Databases in form of OLTP (Online Transactional Database) which houses all the data collected during regular operational hours, and from different sections of the business.
  
  One of the proposed solutions for this problem business face when looking for a solution that implements data-driven decision systems, is to first unify disparate data systems across the organization into a single repository. This Repository is the Enterprise data warehouse and serves as a data-driven reporistry for every business data that can be used to understand the drivers of success for the business. In its minimal form, it can be used for decriptive analytics where the historical nature of the data, can help understand business success based on past data points, and at its most powerful fucntional use, acts as a prescriptive analytical 'partner" where the data can be combined with machine learning models to derive insights about future performance based on current business performance.
    
### About Project
  
     This Project aims to explain the processes involed in building data warehouses to organizations looking to build their first Enterprise Data warehouse (EDW), assuming they currently have a data repositiory which can be used as the data source for the ETL (Extract, Transform and Load) pipelines. 
     The OLTP source used for this project is the Northwind Database, which is representative of a small compnay or a department within a large organization. Using this Database illustrates the processes of converting an OLTP Database to an Enterprise data Warehouse Using SQL Server Integration Services (SSIS) 
     
    Northwind Database Diagram
    
  ![NorthWInd OLTP Diagram](https://user-images.githubusercontent.com/105971126/235525453-37222ea7-2c23-4eb8-a57e-735fff2483e5.png) 

First step is to determine the Fact and Dimensions table for the Data warehouse. Scalability is the watchword of the Data warehouse and the best way to create the data model is through Dimensional Modelling, where there are Fact and Dimensions table. The Fact Table contain quantitative measurements of the business processes and tran sactions while the Dimension Table contain qualitative descriptions about the business itself.

For the Northwind DW, the Fact Table is the SalesOrder Table, which will contain the Primary Key from all other Tables.
The Dimensions Table are Employees, Customers, Suppliers, Products (including Categories), Shippers and Territories.

Next Step is to create Views using the Table relationships to create the staging tables.

### SQL Queries

**Fact SalesOrders Table**

CREATE VIEW FactSalesOrders_Staging
AS
SELECT Orders.OrderID, Customers.CustomerID, Employees.EmployeeID, Shippers.ShipperID, Territories.TerritoryID, 
		Suppliers.SupplierID, Products.ProductID, 
		Orders.OrderDate, Orders.RequiredDate, Orders.ShippedDate, Orders.ShipVia, Orders.Freight, Orders.ShipName, 
        Orders.ShipAddress, Orders.ShipCity, Orders.ShipRegion, Orders.ShipPostalCode, Orders.ShipCountry, 
		[Order Details].UnitPrice, [Order Details].Quantity, [Order Details].Discount
FROM   Region 
INNER JOIN
             Territories ON Region.RegionID = Territories.RegionID 
INNER JOIN
             EmployeeTerritories ON Territories.TerritoryID = EmployeeTerritories.TerritoryID 
INNER JOIN
             Customers 
INNER JOIN
             Orders ON Customers.CustomerID = Orders.CustomerID 
INNER JOIN
             Employees ON Orders.EmployeeID = Employees.EmployeeID 
INNER JOIN
             [Order Details] ON Orders.OrderID = [Order Details].OrderID 
INNER JOIN
             Products ON [Order Details].ProductID = Products.ProductID 
INNER JOIN
             Shippers ON Orders.ShipVia = Shippers.ShipperID 
INNER JOIN
             Suppliers ON Products.SupplierID = Suppliers.SupplierID 
		ON   EmployeeTerritories.EmployeeID = Employees.EmployeeID
  
**Dim Territories**

CREATE VIEW DimTerritories_Staging
AS SELECT Territories.TerritoryID, 
		Territories.TerritoryDescription, 
		Region.RegionDescription
FROM   Region 
INNER JOIN
Territories ON Region.RegionID = Territories.RegionID

**Dim Suppliers**

CREATE VIEW DimSuppliers
AS SELECT SupplierID, CompanyName, ContactName, ContactTitle, Address, City, Region, 
PostalCode, Country, Phone, Fax, HomePage
FROM   Suppliers

**Dim Shippers**

CREATE VIEW DimShippers_Staging
AS SELECT ShipperID, CompanyName, Phone
FROM   Shippers

**Dim Products**

CREATE VIEW DimProducts_Staging
As SELECT Products.ProductID, Products.ProductName, Categories.CategoryName, 
		Categories.De88scription, Products.QuantityPerUnit, Products.UnitPrice, Products.UnitsInStock, 
		Products.UnitsOnOrder, Products.ReorderLevel, Products.Discontinued
FROM   Categories INNER JOIN
             Products ON Categories.CategoryID = Products.CategoryID
             
**Dim EMployees**

CREATE VIEW DimEmployees_Staging
AS SELECT EmployeeID, LastName, FirstName, BirthDate, HireDate, Address, 
City, Region, PostalCode, Country, HomePhone, Extension, Notes, ReportsTo
FROM   Employees


**Dim Customers**

CREATE VIEW DimCustomers
AS SELECT CustomerID, CompanyName, ContactName, ContactTitle, Address, 
City, Region, PostalCode, Country, Phone, Fax
FROM   Customers
