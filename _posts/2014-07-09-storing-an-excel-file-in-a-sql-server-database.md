---
title: "Storing an Excel File in a SQL Server Database"
date: "2014-07-09"
categories: 
  - "sql-server"
---

If you have a table with an [image](http://msdn.microsoft.com/en-us/library/ms187993(v=sql.105).aspx) data type field where you store an Excel file or any file for that matter, and you need to update a particular record with a new file, you can use [OPENROWSET](http://msdn.microsoft.com/en-us/library/ms190312(v=sql.105).aspx).

UPDATE MyTable
SET MyImageField = (
    SELECT \* 
    FROM OPENROWSET(BULK N'C:\\MyExcelFile.xls', SINGLE\_BLOB) AS MyFile
)
FROM MyTable
WHERE ...

 

 

One disadvantage of using this is that the file you are storing needs to be accessible by the SQL Server.
