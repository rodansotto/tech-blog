---
title: "SQL Server 2005: Inserting DEFAULT values"
date: "2007-05-05"
categories: 
  - "sql-server"
---

You can insert a **DEFAULT** value for a column instead of a **NULL** value if the column has a default value defined in it:

    [INSERT](http://search.microsoft.com/default.asp?so=RECCNT&siteid=us%2Fdev&p=1&nq=NEW&qu=INSERT&IntlSearch=&boolean=PHRASE&ig=01&i=09&i=99) [INTO](http://search.microsoft.com/default.asp?so=RECCNT&siteid=us%2Fdev&p=1&nq=NEW&qu=INTO&IntlSearch=&boolean=PHRASE&ig=01&i=09&i=99) [Table](http://search.microsoft.com/default.asp?so=RECCNT&siteid=us%2Fdev&p=1&nq=NEW&qu=Table&IntlSearch=&boolean=PHRASE&ig=01&i=09&i=99)1 ([Column](http://search.microsoft.com/default.asp?so=RECCNT&siteid=us%2Fdev&p=1&nq=NEW&qu=Column&IntlSearch=&boolean=PHRASE&ig=01&i=09&i=99)1, [Column](http://search.microsoft.com/default.asp?so=RECCNT&siteid=us%2Fdev&p=1&nq=NEW&qu=Column&IntlSearch=&boolean=PHRASE&ig=01&i=09&i=99)2)
    [VALUES](http://search.microsoft.com/default.asp?so=RECCNT&siteid=us%2Fdev&p=1&nq=NEW&qu=VALUES&IntlSearch=&boolean=PHRASE&ig=01&i=09&i=99) ([DEFAULT](http://search.microsoft.com/default.asp?so=RECCNT&siteid=us%2Fdev&p=1&nq=NEW&qu=DEFAULT&IntlSearch=&boolean=PHRASE&ig=01&i=09&i=99), N'Some Value')
