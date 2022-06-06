---
title: "SQL Server: Quickly run a command on each database.  How?"
date: "2014-10-07"
categories: 
  - "sql-server"
---

Well it so happens that there is an undocumented stored procedure that you can use to do so and has been in SQL Server for some time now.  This will definitely be handy if you are a software developer that does not like to code with cursor in SQL.  I tested this in SQL Server 2008 R2 and the stored procedure is still there.  Remind you that this stored procedure is undocumented and probably not supported and thus might not exist in future versions of SQL Server.  And there is also a version for table as well.  Pretty cool eh.  See sample usage below.

\-- execute the following command on each database
EXEC sp_MSforeachdb 'PRINT ''?'''
    
\-- execute the following command on each table in the database
USE MyDatabase
EXEC sp_MSforeachtable 'PRINT ''?''';
    
\-- the following uses a filter
\-- it makes sure command will not execute on master, tempDB, model, and msdb
EXEC sp_MSforeachdb '
IF ''?''  NOT IN (''master'', ''tempDB'', ''model'', ''msdb'')
BEGIN
       PRINT ''?''
END'

 

 

Below are links to more information:

- [The undocumented sp_MSforeachdb procedure](http://weblogs.sqlteam.com/joew/archive/2008/08/27/60700.aspx)
- [The undocumented sp_MSforeachtable procedure](http://weblogs.sqlteam.com/joew/archive/2007/10/23/60383.aspx)
- [SQL Server: Applying Filter on sp_MSforeachDB](http://www.codeproject.com/Articles/459536/SQL-Server-Applying-Filter-on-sp-MSforeachDB)
