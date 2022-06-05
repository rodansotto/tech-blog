---
title: "Column aliases in ORDER BY works on older SQL version but not on SQL 2014?"
date: "2016-05-26"
categories: 
  - "sql-server"
---

![]({{ site.baseurl }}/assets/images/sqllogo1.png)

The rule of thumb is: don't prefix the column aliases with a table name or table alias in the ORDER BY clause, OR just use the column name directly instead.  This [MSDN article](https://msdn.microsoft.com/en-us/library/ee240807(v=sql.120).aspx) explains it in detail.


