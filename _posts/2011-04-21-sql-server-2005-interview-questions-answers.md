---
title: "SQL Server 2005: Interview Q&A"
date: "2011-04-21"
categories: 
  - "sql-server"
---

I recently had a technical interview and the following questions gave me a  hard time:

- How many non-clustered indexes can you have?  I know you can only have 1 clustered index but I have no idea for the non-clustered.  The answer is **249**.  But in SQL Server 2008, this number was increased to 999.
- Which among the 2 key constraints allow you to have a **NULL** value, **PRIMARY KEY** or **UNIQUE**?  I know primary keys should not be null, and I am right.  The **UNIQUE** constraint will allow you to add only one NULL value and more than that will be considered as duplicate.
- How do you add a **DEFAULT** constraint in an existing table using SQL?  You could easily do this on the SQL Server Management Studio, but since it’s asking for the SQL, it should look like the following:
    
    \[sourcecode language="sql" padlinenumbers="true" autolinks="true" gutter="false" light="true" toolbar="false"\]
    ALTER TABLE MyTable 
      ADD CONSTRAINT MyConstraint 
        DEFAULT 'MyDefault' FOR MyColumn
    \[/sourcecode\]
    

- What are the T-SQL statements used for transactions?  These should be **BEGIN TRAN**, **COMMIT TRAN**, **ROLLBACK TRAN**, and **SAVE TRAN**.  The SAVE TRAN is like a bookmark or a save point.  You can roll back to a save point.

- What is a **RANK()** function?  This one I have never used.  It is a built-in function in T-SQL under the Ranking Functions category.  For more information, click [here](http://msdn.microsoft.com/en-us/library/ms176102(v=SQL.90).aspx).

- What is a **ROLLUP** operator?  Again I have never used this.  It is used to summarize data.  I probably will have to get familiar with this since I do lots of reporting.  It might make my SQL statements shorter.  For more information, click [here](http://msdn.microsoft.com/en-us/library/ms191500(v=SQL.90).aspx).
