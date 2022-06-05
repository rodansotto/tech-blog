---
title: "SQL Server 2005: Transaction log"
date: "2007-03-26"
categories: 
  - "sql-server"
---

There are actually 2 files that make up a database in SQL Server, one containing the data itself, and the other one containing the transaction logs.  All data inserts, updates, and deletes happen in transaction log file first and stay there until one point in time when they propagate to the actual database itself.  How long will they be in the transaction log file is something I don't know but I'm guessing it might be in milliseconds so you don't notice that your data is being held in the transaction log file first.
