---
title: "SQL Server: Common Table Expression (CTE), ROW_NUMBER(), RANK(), Derived Table, OPENXML()"
date: "2013-05-08"
categories: 
  - "sql-server"
---

- **Common Table Expression (CTE)** is easy to use since you don’t have to create a table or even drop them after use and you can reference it multiple times and anywhere in the query.  You would use it like this in it’s simplest form:
    
    WITH Table2 AS
    (
        SELECT *
        FROM Table1
    )
    SELECT *
    FROM Table2
    
     
    

 

- **ROW_NUMBER()** and **RANK()** is useful in numbering or ranking the records based on a criteria.  Both of them are used pretty much the same way and below is an example of using **RANK()** in it’s simplest form:
    
    SELECT *, RANK() OVER(ORDER BY Grade DESC) AS StudentRank
    FROM StudentGrades
    
     
    

 

- **Derived Table** allows you to substitute a query in place of a table in the **FROM** or **JOIN** clause for example.  Below is one such use:
    
    SELECT *
    FROM
    (
        SELECT *
        FROM Table1
    ) AS Table2
    
     
    

 

- **OPENXML()** is useful if you want to view your XML data in a series of rows and columns pretty much like a table.  For more information, click [here](http://msdn.microsoft.com/en-us/library/ms186918(v=sql.90).aspx)
