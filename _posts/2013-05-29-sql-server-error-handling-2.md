---
title: "SQL Server: Error Handling"
date: "2013-05-29"
categories: 
  - "sql-server"
---

**Error handling** in SQL Server is similar to C#’s exception handling.  Syntax is below:

BEGIN TRY
    \-- this is where you put your statements
END TRY
BEGIN CATCH
    \-- this is where you handle the error
END CATCH

 

 

And of course you can get more information about the error using the following:

- **ERROR_PROCEDURE()** – returns name of stored procedure or trigger where the error occurred
- **ERROR_LINE()** – returns the line number in the procedure or trigger where the error occurred
- **ERROR_NUMBER()** – returns the error number
- **ERROR_MESSAGE()** – returns the error message

 

The following might also be useful in handling your errors:

- **@@TRANCOUNT** – holds the # of transactions ongoing; useful if you are using transactions and want to know if you have pending transactions after catching an error (**IF @@TRANCOUNT > 0**) so you can maybe rollback
- **@@PROCID** – returns the object ID of the current stored procedure, UDF, or trigger
- **OBJECT_NAME()** – returns the name of the database object referred to by the object ID; passing **@@PROCID** will return the name of the current stored procedure, UDF, or trigger (**OBJECT_NAME(@@PROCID**)
- **USER_NAME()** – returns database user name (e.g. **dbo**); for more info go [here](http://msdn.microsoft.com/en-us/library/ms188014(v=sql.110).aspx)
- **SYSTEM_USER** – returns the current Windows or SQL Server login name depending on how the user is logged in; for more info go [here](http://msdn.microsoft.com/en-us/library/ms179930(v=sql.110).aspx)
