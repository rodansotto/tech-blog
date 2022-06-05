---
title: "SQL Tricks: CSV To Table Rows And Vice Versa"
date: "2017-10-12"
categories: 
  - "sql-server"
---

![]({{ site.baseurl }}/assets/images/sqllogo1.png) I was looking for a one-line SQL statement to convert a comma-separated value list string to table rows and vice-versa and below is what I found.  I prefer not to put logic in my SQL code (I prefer to limit it with just the simple CRUD statements) but if no other choice then these two SQL tricks will come in handy.  You can try to execute this SQL query on any online SQL compiler you can find on the Internet, but I would recommend [rextester's sql compiler](http://rextester.com/l/sql_server_online_compiler)

.

```sql
-- So if you have a comma separated list, for example a list of integers
DECLARE @MyListOfInts VARCHAR(255) = '123,456,789'

-- Use the following SQL trick to parse them to table rows
-- Basically you convert the CSV to XML first and use the nodes() method to shred the XML into relational data
SELECT List.Item.value('.', 'INT')
FROM
(
    SELECT CAST('<List><Item>' + REPLACE(@MyListOfInts,',','</Item><Item>') + '</Item></List>' AS XML) AS ListXML
) ListXMLTable
CROSS APPLY ListXMLTable.ListXML.nodes('/List/Item') List(Item)

-- And if you have values in table rows that you want to convert to CSV...
-- The following SQL trick will do it for you
-- Basically the inner SELECT query with unnamed column and with FOR XML PATH('') converts the 
-- table row values to XML without any tags and the SUBSTRING() function in the outer SELECT query
-- just removes the leading comma character
SELECT SUBSTRING
(
    (
        SELECT ',' + CAST(List.Item AS VARCHAR(MAX))
        FROM
        (
            SELECT 123 AS Item UNION SELECT 456 UNION SELECT 789
        ) List
        ORDER BY List.Item
        FOR XML PATH('')
    )
    ,2
    ,1000
)
```
