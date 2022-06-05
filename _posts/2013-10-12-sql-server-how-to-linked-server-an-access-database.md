---
title: "SQL Server: How to Linked Server an Access Database"
date: "2013-10-12"
categories: 
  - "ms-access"
  - "sql-server"
---

Below is the script to create a linked server to an Access database:

EXEC master.dbo.sp\_addlinkedserver   
    @server = N'MyLinkedServerAccessDB',   
    @srvproduct = N'Access',   
    @provider = N'Microsoft.Jet.OLEDB.4.0',   
    @datasrc = N'C:\\MyAccessDB.mdb'  

Plus you also need to create the linked server login.  What’s important to note here is that the password for the admin account in the Access database is blank by default, unless you have set the password.

EXEC master.dbo.sp\_addlinkedsrvlogin   
    @rmtsrvname = N'MyLinkedServerAccessDB',  
    @useself = N'False',  
    @locallogin = N'sa',  
    @rmtuser = N'admin',  
    @rmtpassword = ''
