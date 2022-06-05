---
title: "SQL Server: Quick Notes on SYNONYM, MERGE, TRY_CONVERT, TRY_CAST, PARSE, TRY_PARSE, CHECKSUM, ISNULL, COALESCE, NULLIF, and JOIN"
date: "2014-01-15"
categories: 
  - "sql-server"
---

**SYNONYM**

Starting in SQL Server 2005, you can use **[SYNONYM](http://msdn.microsoft.com/en-us/library/ms191230(v=sql.90).aspx)** in place of their referenced object in SQL statements.  It’s like an alias.  The benefit here is that if you decide to alter the name of the object being referenced by the synonym, let’s say you want to change the name of the table or use a totally different table, or change the location of the table, all you have to do is update the synonym to use the correct table and all the SQL statements using the synonym shouldn’t have to be changed at all.

\-- say for example you have the following synonym,
\-- where ClientToronto is the database name
CREATE SYNONYM SYN\_CUSTOMERS FOR ClientToronto.dbo.Customers
GO
\-- 
\-- and you have a SQL statement that uses that synonym
SELECT \* FROM SYN\_CUSTOMERS
\-- 
\-- if you ever need to run the same SQL statement for a different client,
\-- say for a client in Chicago, all you have to do is update the synonym
\-- to point to a different database
DROP SYNONYM SYN\_CUSTOMERS
GO
CREATE SYNONYM SYN\_CUSTOMERS FOR ClientChicago.dbo.Customers
GO
\--
\-- to check which object the synonym is referring to, 
\-- you can use the system view sys.synonyms
SELECT BASE\_OBJECT\_NAME FROM sys.synonyms WHERE NAME = 'SYN\_CUSTOMERS'

 

 

**MERGE**

Starting in SQL Server 2008, if you want to update a target table based on a source table, which will involve inserting new records and updating or deleting existing records on the target table, you can use **[MERGE](http://msdn.microsoft.com/en-us/library/bb510625(v=sql.105).aspx)** and it will perform an **INSERT** and **UPDATE/****DELETE** operations on the target table in a single statement, instead of using each operation separately.

MERGE Customers AS TARGET
USING (SELECT CustomerCode, CustomerName FROM ImportCustomers) 
    AS SOURCE (CustomerCode, CustomerName)
ON TARGET.CustomerCode = SOURCE.CustomerCode
WHEN MATCHED THEN 
    \-- do an update when importing existing customers
    UPDATE SET TARGET.CustomerName = SOURCE.CustomerName
WHEN NOT MATCHED THEN 
    \-- do an insert when importing new customers
    INSERT (CustomerName, CustomerCode)
    VALUES (SOURCE.CustomerName, SOURCE.CustomerCode)
; 
\-- note that the semicolon is required at the end of the MERGE statement

 

 

**TRY\_CONVERT, TRY\_CAST, PARSE, TRY\_PARSE**

If you want to avoid getting an error when using **CONVERT** or **CAST**, use **[TRY\_CONVERT](http://msdn.microsoft.com/en-us/library/hh230993.aspx)** and **[TRY\_CAST](http://msdn.microsoft.com/en-us/library/hh974669.aspx)**.  These functions, which unfortunately are available only in SQL Server 2012, return NULL if the conversion or casting failed.  New in SQL Server 2012 too are **[PARSE](http://msdn.microsoft.com/en-us/library/hh213316.aspx)** and **[TRY\_PARSE](http://msdn.microsoft.com/en-us/library/hh213126.aspx)** functions, used only for converting from string to date/time and number types, much like the **TryParse()** method in C#, if you know C#.

SELECT TRY\_CONVERT(DATETIME2, '1/1/2014')
SELECT TRY\_CAST('1/1/2014' AS DATETIME2)
SELECT TRY\_PARSE('1/1/2014' AS DATETIME2)

 

 

**CHECKSUM**

The [**CHECKSUM**](http://msdn.microsoft.com/en-us/library/ms189788(v=sql.90).aspx) function has been around since SQL Server 2005.  It’s main use is in building hash indexes.  But it can also be useful in synchronizing your data.  Let’s say you have 2 tables that you want to sync.  You can create a checksum value computed over a list of fields in your record whose changes you want to keep track of.  If a record’s checksum value is different, then sync the record.

 

**ISNULL, COALESCE, NULLIF**

You would think that **[ISNULL](http://msdn.microsoft.com/en-us/library/ms184325(v=sql.90).aspx)** function will return true if the expression is NULL.  But actually it replaces NULL with the specified replacement value and returns that value.  If it’s not NULL, it returns back the expression.  Much like **[COALESCE](http://msdn.microsoft.com/en-us/library/ms190349(v=sql.90).aspx)**, but COALESCE accepts multiple expressions and return the first non NULL expression.  Now **[NULLIF](http://msdn.microsoft.com/en-us/library/ms177562(v=sql.90).aspx)** is a totally different function, in that it returns a NULL value if the two specified expressions are equal.

 

**JOIN**

I already talked about SQL Server joins in this [post](http://rodansotto.wordpress.com/2007/05/05/sql-server-2005-joins-and-union/).  But for a visual description, click [here](http://www.codeproject.com/KB/database/Visual_SQL_Joins/Visual_SQL_JOINS_orig.jpg).
