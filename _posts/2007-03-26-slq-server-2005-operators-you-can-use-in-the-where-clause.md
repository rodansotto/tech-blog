---
title: "SLQ Server 2005: Operators you can use in the WHERE clause"
date: "2007-03-26"
categories: 
  - "sql-server"
---

Besides the standard comparison operators (**\=**, **\>**, **<**, etc.), the boolean operators (**AND**, **OR**, **NOT**) and the **BETWEEN** operator, you can also use **LIKE**, **IN**, **ALL**, **ANY**, **SOME**, and **EXISTS**.

**LIKE**

Use this when you want to match the value of a column to a string with wildcard characters specified after this keyword.  You use **%** to mean 1 or more characters and **_** to mean just 1 character.  Enclosing characters in **\[\]** indicates that any of the characters inside is OK.  Specifying **^** before a character excludes that character.

**IN**

Use this if you want to match the value of a column to a list of values specified after this keyword.  You can also use this with subqueries.

**ALL, ANY, SOME**

Used in conjunction with a comparison operator (e.g. =, >, <).  Use this if you want to compare the value of a column to all, any or some of the values in a subquery.

Below is an example usage (the default is ALL):

<column | expression> (comparison operator) <ANY | SOME> (subquery)

**EXISTS**

Use this to check if a subquery returns at least 1 row.
