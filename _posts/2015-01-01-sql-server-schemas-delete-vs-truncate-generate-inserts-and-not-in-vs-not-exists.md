---
title: "SQL Server: Schemas, DELETE vs. TRUNCATE, Generate INSERTs, and NOT IN vs. NOT EXISTS"
date: "2015-01-01"
categories: 
  - "sql-server"
---

**Schemas**

[Data Organization Using Schemas](http://dataeducation.com/blog/data-organization-using-schemas) best explains with clear examples what schema in SQL Server is.  Important things to note are:

- Schemas were first introduced in SQL Server 2005.

- _dbo_ in pre SQL Server 2005 was used as the default database owner but now it is used as the default schema.

- Schema is analogous to namespace (as in namespace in C#), or a container used to store database objects.

- Schema owner can be a Windows domain login, Windows local login, SQL Server login, Windows group, database role, server role, or application role.

- Schemas are simpler to manage in terms of permissions and security.

- Lastly, schemas can provide logical boundaries without the need to create multiple physical databases.

- Additional readings:
    - [Benefits of using Schema’s in SQL Server 2005/2008](http://www.praveenmodi.com/advantage-and-use-of-schemas-over-object-owners-in-sql-server-2005/)
    
    - [SQL Server Best Practices – Implementation of Database Object Schemas](http://technet.microsoft.com/en-us/library/dd283095(v=sql.100).aspx)

**DELETE vs. TRUNCATE**

Sometimes deleting so many rows in a SQL Server table takes up a loooong time.  If rolling back data does not matter, use TRUNCATE instead.

```sql TRUNCATE TABLE dbo.MyTable ```

**Generate INSERTs**

I used to use a script I got from the Internet that generates INSERT statements from a table so I can repopulate the table next time with same data, or populate a similar table in another database for example.  Recently I found another alternative in SQL Server Management Studio with the _Generate Scripts..._ database task.  Just right-click on the database where the table you want to generate INSERTs from is, go to _Tasks_, and click _Generate Scripts..._.  Go over the steps and make sure on the scripting options, by clicking the _Advanced_ button, that you select _Data only_ for the _Types of data to script_ under the _General_ options.  This will generate the INSERT statements.

**NOT IN vs. NOT EXISTS**

```sql SELECT ProductID FROM Products WHERE ProductID NOT IN ( SELECT ProductID FROM OrderDetails )

\-- versus

SELECT ProductID FROM Products p WHERE NOT EXISTS ( SELECT 1 FROM OrderDetails od WHERE od.ProductID = p.ProductID ) ```

I am not talking about the performance difference between these two SQL operations but rather the functional difference between them.  It might be tempting to say they are the same but it is not.  NOT IN will not behave as one expects when the column used for comparison in the subquery contains NULL values (OrderDetails.ProductID in the example above).  The article [NOT EXISTS vs NOT IN](http://sqlinthewild.co.za/index.php/2010/02/18/not-exists-vs-not-in/) explains why.

- Additional readings:
    - [SQL Server: JOIN vs IN vs EXISTS - the logical difference](http://weblogs.sqlteam.com/mladenp/archive/2007/05/18/60210.aspx)
    
    - [NOT IN vs NOT EXISTS (from stackoverflow)](http://stackoverflow.com/questions/173041/not-in-vs-not-exists)
