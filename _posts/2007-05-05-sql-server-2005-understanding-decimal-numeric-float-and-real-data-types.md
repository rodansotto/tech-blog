---
title: "SQL Server 2005: Understanding decimal, numeric, float, and real data types"
date: "2007-05-05"
categories: 
  - "sql-server"
---

Since I came from a VB background, I get confused when I encounter these data types in SQL Server.  In VB if I need to use a variable that can hold a number with digits to the right of the decimal point, I declare the variable as **single** or **double**.  In SQL Server, you have **decimal**, **numeric**, **float** and **real** to choose from.  So what is the difference between them?

**Decimal and numeric**

Decimal and numeric are called **exact numerics** in SQL Server because they have fixed **precision** and **scale**. 

**Precision** is the maximum total number of digits that can be stored, both to the left and to the right of the decimal point.  The value for precision can be from **1** to **38**.

**Scale** is the maximum number of digits that can be stored to the right of the decimal point.  The value for scale can be from **0** to **precision**.

If you don't specify the precision and scale when you declare the variable as decimal or numeric, by default it will have a precision of 18 digits and a scale of 0 digit.  It's like declaring it as:

[decimal](http://search.microsoft.com/default.asp?so=RECCNT&siteid=us%2Fdev&p=1&nq=NEW&qu=decimal&IntlSearch=&boolean=PHRASE&ig=01&i=09&i=99) (18, 0)

Since decimal and numeric are both the same, either numeric or decimal will do.

If you are concerned with storage, then use a precision of **9 digits or less** and this will take only **5 bytes**, the minimum for a decimal or numeric.  A precision of **10-19 digits** will give you **9 bytes**; **20-28 digits** will give you **13 bytes**; and **29-38** digits will give you **17 bytes**.

**Float and real**

Float and real are called **approximate numerics** and are used for floating point numeric data (whatever that means).  Since decimal or numeric will serve my purpose if all I want is a number that can store digits to the right of the decimal point, then I don't need to bother with float and real unless I am working on a mathematical application.
