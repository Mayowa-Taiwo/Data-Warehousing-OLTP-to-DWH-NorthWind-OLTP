### IMPLEMENTING A DATA-DRIVEN DECISION SYSTEM PART 1

**Introduction**
 
 As more organization begin to look for ways to maximise their business' potential, improve operations and return on Investments, they begin by seeking ways to integrate data-driven decision making into daily operations to uncover insights, there's the initial confusion and exasperation regarding the starting point. A a standard practice, most businesses have data repositories in form of ERP (Enterprise Resource Planning) systems, Relational Databases in form of OLTP (Online Trnasactional Database) which houses all the data collected during regular operational hours, and from different sections of the business.
  
  One of the proposed solutions for this problem business face when looking for a solution that implements data-driven decision systems, is to first unify disparate data systems across the organization into a single repository. This Repository is the Enterprise data warehouse and serves as a data-driven reporistry for every business data that can be used to understand the drivers of success for the business. In its minimal form, it can be used for decriptive analytics where the historical nature of the data, can help understand business success based on past data points, and at its most powerful fucntional use, acts as a prescriptive analytical 'partner" where the data can be combined with machine learning models to derive insights about future performance based on current business performance.
  
  
  **About Project**
     This Project aims to explain the processes involed in building data warehouses to organizations looking to build their first Enterprise Data warehouse (EDW), assuming they currently have a data repositiory which can be used as the data source for the ETL (Extract, Transform and Load) pipelines. 
     The OLTP source used for this project is the Northwind Database, which is representative of a small compnay or a department within a large organization.
     
    Northwind Database Diagram
    
  ![NorthWInd OLTP Diagram](https://user-images.githubusercontent.com/105971126/235525453-37222ea7-2c23-4eb8-a57e-735fff2483e5.png) 

