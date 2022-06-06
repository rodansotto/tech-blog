---
title: "SQL Server 2005: INFORMATION_SCHEMA views"
date: "2007-05-05"
categories: 
  - "sql-server"
---

You can use the **INFORMATION_SCHEMA** views to get the metadata on any database:

<table border="0" cellspacing="0" cellpadding="0" width="400"><tbody><tr><td valign="top" width="400"><a style="color:#0000ff;" href="http://search.microsoft.com/default.asp?so=RECCNT&amp;siteid=us%2Fdev&amp;p=1&amp;nq=NEW&amp;qu=SELECT&amp;IntlSearch=&amp;boolean=PHRASE&amp;ig=01&amp;i=09&amp;i=99"><font size="2" face="Courier New">SELECT</font></a><font size="2" face="Courier New"> * </font><a style="color:#0000ff;" href="http://search.microsoft.com/default.asp?so=RECCNT&amp;siteid=us%2Fdev&amp;p=1&amp;nq=NEW&amp;qu=FROM&amp;IntlSearch=&amp;boolean=PHRASE&amp;ig=01&amp;i=09&amp;i=99"><font size="2" face="Courier New">FROM</font></a><font size="2" face="Courier New"> INFORMATION_SCHEMA.TABLES</font></td></tr></tbody></table>

You can also get information on table columns, table constraints, etc.  You can check what views are available by going to the **System Views** node under the **Views** node of the database from the **Microsoft SQL Server Management Studio**.
