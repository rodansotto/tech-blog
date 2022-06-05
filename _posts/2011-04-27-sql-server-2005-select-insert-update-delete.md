---
title: "SQL Server 2005: SELECT, INSERT, UPDATE, DELETE"
date: "2011-04-27"
categories: 
  - "sql-server"
---

The parts of a **SELECT** statement are:

\[sourcecode language="sql" gutter="false" light="true" toolbar="false"\]
SELECT 
FROM 
WHERE 
GROUP BY 
HAVING 
ORDER BY 
FOR XML
OPTION
\[/sourcecode\]

By default, **ALL** is assumed in **SELECT**, thus including every row.  Using **SELECT DISTINCT** excludes duplicate rows.  Note that you can also use **DISTINCT** in aggregate functions, like below:

\[sourcecode language="sql" gutter="false" light="true" toolbar="false"\]
SELECT COUNT (DISTINCT Column)
FROM Table
\[/sourcecode\]

You can use **ORDER BY** on any column on the table even if it is not returned or not part of the **SELECT** list.  The **FOR XML** clause is used for outputting XML data while the **OPTION** clause is for making query hints.

The **INSERT** statement can take either of the two following forms:

\[sourcecode language="sql" gutter="false" light="true" toolbar="false"\]
INSERT INTO Table (Column1, Column2)
VALUES (Value1, Value2)

INSERT INTO Table (Column1, Column2)
SELECT ...
\[/sourcecode\]

Note that the column list are optional on both forms.

The parts of an **UPDATE** statement are:

\[sourcecode language="sql" gutter="false" light="true" toolbar="false"\]
UPDATE
SET
FROM
WHERE
\[/sourcecode\]

An **UPDATE** can be created from multiple tables but only one table is affected, meaning only one table can be the subject of an update action.

The **DELETE** statement has the shortest syntax.  Just provide the table name and optionally a **WHERE** clause.
