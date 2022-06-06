---
title: "SQL Server 2005: Aggregate Functions"
date: "2007-03-27"
categories: 
  - "sql-server"
---

Aggregate functions (e.g. **AVG**, **MIN**, **MAX**, **COUNT**, etc.) can be in a **SELECT** statement without the **GROUP BY** clause.  Without the **GROUP BY** clause in the **SELECT** statement will apply the aggregate function to the entire result set.

Also all aggregate functions, except for **COUNT(*)**, ignore **NULL**s.  So you need to be sure that when you use an aggregate function on a column, you want any **NULL** values in your column to be excluded in the aggregation, meaning they will not be included in the function.
