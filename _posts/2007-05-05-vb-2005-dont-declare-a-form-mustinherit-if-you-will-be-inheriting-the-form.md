---
title: "VB 2005: Don't declare a form MustInherit if you will be inheriting the form"
date: "2007-05-05"
categories: 
  - "vb-net"
---

If you create a form to be inherited and you try to declare a function or procedure as **MustOverride**:

    Protected MustOverride Function MyFunction() As String

you need to declare that form **MustInherit**:

    Public MustInherit Class MyForm

But doing this will prevent you from inheriting the form because you won't see this form on the **Inheritance Picker** tool window when you create an inherited form (**Add New Item... -> Inherited Form**).

You have no choice but to declare  your function or procedure as **Overridable**:

    Protected Overridable Function MyFunction()As String
        ' You can put some code here or nothing at all...
    End Function

and then make sure your derived form overrides this function:

    Protected Overrides Function MyFunction()As String
        ' Your code here...
    End Function
