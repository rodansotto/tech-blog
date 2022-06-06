---
title: "General: On a 64-bit OS/machine, what will be the issues in running your application that uses Access database directly or indirectly using SQL Server’s Linked Server object"
date: "2013-06-09"
categories: 
  - "general"
  - "ms-access"
  - "sql-server"
---

If you have an application, say in **.NET**, that uses an **Access** database in some way or the other, or uses **SQL Server** that in turn links to an Access database through the **Linked Server** object, and you want to run your application and also the SQL Server on a **64-bit** OS/machine, you might be in for a lot of surprises.

 

Here is why:

- The **Microsoft.Jet.OLEDB.4.0** is only available on 32-bit.  Same with **Microsoft.ACE.OLEDB.12.0** if you are using a later version of Access like **2007** and up.  You can still run them on a 64-bit OS/machine in **WoW64** (a subsystem in 64-bit Windows that allows 32-bit applications to run on them).  Only problem is that the application that uses them need to run in 32-bit mode.  So much for running your application on 64-bit eh.  But fear not, there is a solution, although many of you might stay away from it, and that is linking your Access database in SQL Server and  having your application connect to the SQL Server instead.  So now you can run your application in 64-bit mode.

 

- If you have a **SQL Server** that links to an **Access** database through the **Linked Server** object, you cannot install a 64-bit version of SQL Server on a 64-bit OS/machine or else your linked server to the Access database will not work.  You have to install a 32-bit version of the SQL Server.  Yes, that is the only solution, for now, until Microsoft comes up with a 64-bit version of the Access database engine, if that will still come.

 

- If you have created a link to your Access database from your SQL Server, you might encounter a similar collation problem below when running your T-SQL queries involving joins to the linked server Access database:

> Cannot resolve the collation conflict between "Latin1_General_CI_AS" and "SQL_Latin1_General_CP1_CI_AS" in the equal to operation.

 

One way to solve this problem is by adding the **COLLATE DATABASE_DEFAULT** to every text fields that you are comparing with either on the **WHERE** or **JOIN** clause, such as the example below:

SELECT *
FROM 
    SQLServerTable1 s
    INNER JOIN LinkedServerAccessDB...AccessDBTable1 AS a
        ON s.DateField1 = a.DateField1
        AND s.IntField1 = a.IntField1
        AND s.TextField1 COLLATE DATABASE_DEFAULT = a.TextField1 COLLATE DATABASE_DEFAULT
        AND s.TextField2 COLLATE DATABASE_DEFAULT = a.TextField2 COLLATE DATABASE_DEFAULT

 

 

- Be aware that in using a linked server to an Access database that any **DELETE** statements that you execute within a transaction (where you can commit or rollback) will not work (at least for me it did not work) and will give you the below error message:

> The requested operation could not be performed because OLE DB provider "Microsoft.Jet.OLEDB.4.0" for linked server "LinkedServerAccessDB" does not support the required transaction interface.

 

Solution to this is to bring all DELETE statements out of the transaction and execute them after committing the transaction.

 

So that’s it for this topic.  If you have any questions, feel free to comment :).
