---
title: "SQL Server 2005: New data types"
date: "2007-04-28"
categories: 
  - "sql-server"
---

I recently had a job interview and one of the questions in the written exam that they gave me was about the new data types in SQL Server 2005.  I did get most of them.  So here are the new data types in SQL Server 2005, in case you wanted to know:

**XML**

As the name suggests, this data type can store XML data.

**VarChar(MAX), NVarChar(MAX), and VarBinary(MAX)**

These are called large value data types.  By specifying the **MAX** keyword in the VarChar, NVarChar, and VarBinary data types, you essentially increased the storage size of these data types to **2^31 - 1 bytes**.
