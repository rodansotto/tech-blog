---
title: "SQL Server 2005: Bit, Image, VarBinary, and unsigned numeric data types"
date: "2007-03-26"
categories: 
  - "sql-server"
---

**Bit**

If you use bit, say to represent a boolean value, you are actually not allocating 1 bit but **1 byte**.  The first bit will give you 1 byte and the next 7 bits will use that byte so if you declared 8 columns in your table of data type **bit**, they will all share the same byte.  If these are all nullable, or just even one, another byte is allocated.  So if you don't need your bit to be nullable, then make sure it's not.

**Image and **VarBinary****

**Image** data type is used for backwards compatibility in SQL Server 2005 and **varbinary(max)** is the replacement for it, which is essentially a LOB (large text or binary object) field that can take up to **2^31 bytes** of data.  If you don't want this a big of a size, you can specify a length for a **varbinary** data type up to a maximum of **8,000 bytes** only.

**Unsigned numeric data types**

SQL Server 2005 (or SQL Server for that matter) does not have a concept of them.
