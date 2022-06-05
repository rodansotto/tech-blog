---
title: "Always wondered how you can write custom code in SQL Server reports?"
date: "2014-05-08"
categories: 
  - "sql-server"
---

Well there are 2 ways of doing it actually.  One is embedding it inside the report itself, but you are limited to using only VB.NET.  The other one is creating a custom code assembly, either in VB.NET or C#, and referencing it from the report.  If you ask me, I prefer the custom code assembly so I can write it in C#.

The following links go through the step by step of adding custom code:

- [SQL Server Reporting Services Embedding .NET Code for Report Formatting and Error Handling](http://www.mssqltips.com/sqlservertip/3199/sql-server-reporting-services-embedding-net-code-for-report-formatting-and-error-handling/)
- [SQL Server Reporting Services Custom Code Assemblies](http://www.mssqltips.com/sqlservertip/3224/sql-server-reporting-services-custom-code-assemblies/)

For more information on MSDN, click [here](http://msdn.microsoft.com/en-us/library/ms156028(v=sql.105).aspx).
