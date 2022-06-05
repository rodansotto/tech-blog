---
title: "SQL Server: Hiding your prod data and built-in function STUFF()"
date: "2016-06-03"
categories: 
  - "sql-server"
---

![]({{ site.baseurl }}/assets/images/sqllogo1.png)

If you need to use production data for your testing and don't want to expose any sensitive data on your development environment, you should look at obfuscating them.  This [article](https://www.simple-talk.com/sql/database-administration/obfuscating-your-sql-server-data/) shows the common obfuscation methods in use: character scrambling, repeating character masking, numeric variance, nulling, artificial data generation, truncating, encoding, and aggregating.

Also, if you are looking for a function in SQL Server that pretty much does like the function REPLACE() but only replaces one substring in a specific position and length, then [STUFF()](https://msdn.microsoft.com/en-CA/library/ms188043.aspx) might be the one.


