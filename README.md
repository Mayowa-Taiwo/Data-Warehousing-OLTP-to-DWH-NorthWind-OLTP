### END-TO-END ANALYTICS-DRIVEN ENTERPRISE DECISION SOLUTION  PART 1. (IMPLEMENTING AN ENTERPRISE DATA WAREHOUSE USING SSIS)

**Introduction**

 - In today's competitive business landscape, organizations are constantly searching for ways to maximize their potential and improve operations. One popular approach is to integrate data-driven decision-making into daily operations to uncover insights. However, organizations often encounter confusion and frustration when starting the process. Fortunately, most businesses already have data repositories such as ERP (Enterprise Resource Planning) systems and relational databases like OLTP (Online Transactional Database) that store data collected from different areas of the organization during regular operational hours. 
 - To implement data-driven decision systems successfully, one solution is to unify disparate data systems across the organization into a single repository. This repository is known as the enterprise data warehouse, a data-driven repository for all business data to be used for analytical purposes. It enables organizations to understand the drivers of success and provides insight into past performance using descriptive analytics. At its most powerful, the data warehouse acts as a prescriptive analytical 'partner,' combining data with machine learning models to derive insights about future performance based on current business performance.
 - Implementing data-driven decision-making is essential for businesses to succeed in today's competitive landscape. By unifying data systems into a single repository, organizations can unlock the full potential of their data and gain valuable insights into their business operations.
    
### About Project
 - This project aims to explain the processes involved in building data warehouses for organizations looking to create their first Enterprise Data Warehouse (EDW), assuming they currently have a data repository that can be used as the data source for the ETL (Extract, Transform, and Load) pipelines. The OLTP source used for this project is the Northwind Database, which represents a small company or department within a large organization. This database serves as an example for converting an OLTP Database to an Enterprise Data Warehouse using SQL Server Integration Services (SSIS)."
     
									Northwind Database Diagram
    
  ![NorthWInd OLTP Diagram](https://user-images.githubusercontent.com/105971126/235525453-37222ea7-2c23-4eb8-a57e-735fff2483e5.png) 

First step is to determine the Fact and Dimensions table for the Data warehouse. Scalability is the watchword of the Data warehouse and the best way to create the data model is through Dimensional Modelling, where there are Fact and Dimensions table. The Fact Table contain quantitative measurements of the business processes and tran sactions while the Dimension Table contain qualitative descriptions about the business itself.

For the Northwind DW, the Fact Table is the SalesOrder Table, which will contain the Primary Key from all other Tables.
The Dimensions Table are Employees, Customers, Suppliers, Products (including Categories), Shippers and Territories.

Next Step is to create Views using the Table relationships to create the staging tables.


