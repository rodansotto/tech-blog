---
title: "Access: Type Mismatch Run-time Error After Converting to ACCDB Format"
date: "2014-06-03"
categories: 
  - "ms-access"
---

You might receive a _Run-time error '13': Type mismatch_ after converting a Microsoft Access database from .mdb to .accdb format.  The solution might be as easy as removing the reference to the ADO object library, if you are not using it.

- Open the Access database in question.
- Open the Visual Basic Editor (VBE) by pressing ALT+F11.
- On the Tools menu, click References.
- In the References dialog box, uncheck Microsoft ActiveX Data Objects, and click OK.
