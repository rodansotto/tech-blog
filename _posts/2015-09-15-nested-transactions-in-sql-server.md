---
title: "Nested Transactions in SQL Server"
date: "2015-09-15"
categories: 
  - "sql-server"
---

If you have a stored proc that executes a bunch of SQL statements inside a transaction because they are all meant to be executed as one atomic transaction and needs to be executed as quick as possible to avoid blocking too long others who want to call this stored proc, then you need to make sure this stored proc is not nested in another transaction.  Because nested transactions in SQL server is different than the nesting concept that you might have been accustomed to in a programming language, say in C#.

\[code language="sql" light="true"\]
-- Say for example you need to write to a field in a table
CREATE TABLE \[dbo\].\[TestTable\](
	\[TestField1\] \[nchar\](10) NULL
) ON \[PRIMARY\]
GO

-- And it needs to be in a transaction, so you created a stored proc below
CREATE PROCEDURE \[dbo\].\[usp\_TestInnerTrans\] 
AS
BEGIN
	BEGIN TRANSACTION
		INSERT INTO \[dbo\].\[TestTable\] (\[TestField1\]) VALUES ('Value1')
	COMMIT TRANSACTION
END
GO

-- When you call this stored proc directly, say using EXEC, 
-- you can get at most a 1 sec exec time

-- Now what if you have another stored proc that calls usp\_TestInnerTrans 
-- nested inside another transaction

-- Below is that other stored proc and let's say it takes 10 secs to finish 
-- and commit the outer transaction
CREATE PROCEDURE \[dbo\].\[usp\_TestOuterTrans\] 
AS
BEGIN
	BEGIN TRANSACTION
	EXEC usp\_TestInnerTrans
	WAITFOR DELAY '00:00:10'
	COMMIT TRANSACTION
END
GO

-- What happens is that any other process that calls usp\_TestInnerTrans 
-- will block and will wait until usp\_TestOuterTrans finishes, 
-- which is 10 secs and not 1 sec.
\[/code\]

  

As you can see inner transactions are ignored and the outermost transaction becomes the only one true transaction.  [SQL Server Transaction Locking and Row Versioning Guide](https://technet.microsoft.com/en-us/library/jj856598(v=sql.110).aspx#Advanced) has a section on nested transactions that explains it better.  It's a great article so I recommend reading it from start to finish.

![](/technical-blog/assets/images/sqllogo1.png)


