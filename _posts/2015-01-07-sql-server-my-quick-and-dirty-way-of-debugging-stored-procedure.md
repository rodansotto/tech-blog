---
title: "SQL Server: My Quick and Dirty Way of Debugging Stored Procedure"
date: "2015-01-07"
categories: 
  - "sql-server"
---

I use the below SQL script to debug a stored procedure in chunks, replacing or adding into it the rest of the stored procedure code until every code checks out fine.  Since I use transactions, changes are temporary and it rolls back the transaction at the end.  I also used the [error handling in SQL Server](https://rodansotto.github.io/tech-blog/2013/05/28/sql-server-error-handling-2.html) to catch and print the error line, error number and error message.

```sql
BEGIN TRANSACTION BEGIN TRY -- -- your SQL code here -- END TRY BEGIN CATCH PRINT 'Error at line # ' + CAST(ERROR_LINE() AS VARCHAR(MAX)) + ': ' + CAST(ERROR_NUMBER() AS VARCHAR(MAX)) + ' - ' + ERROR_MESSAGE() END CATCH IF @@TRANCOUNT > 0 ROLLBACK TRANSACTION 
```
