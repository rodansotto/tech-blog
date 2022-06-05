---
title: "SQL Server 2005: model and msdb system databases"
date: "2007-03-25"
categories: 
  - "sql-server"
---

**model** and **msdb** are among the 2 of the 4 system databases in SQL Server 2005, the other 2 being the **master** and **tempdb**. 

**model** is a template for creating new databases so this is where you might want to add additional objects (e.g. tables, stored procedures, user defined types, etc.) that you want your new databases to have when you create them. 

In my last project I have a user defined type **dbo.boolean** from the **bit** data type and I thought this would be a good candidate to add to the model database.  I went and add this to the model database and created a new **Test** database and lo and behold, I have the **dbo.boolean** user defined data type there.

If you are scheduling jobs on SQL Server 2005, **msdb** database is the place where all the information on them are stored.
