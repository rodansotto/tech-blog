---
title: "VB 2005: The Global keyword"
date: "2007-05-05"
categories: 
  - "vb-net"
---

I was looking at the code generated by Visual Studio and I encounter this **Global** keyword.  Found out that you use this when you want to start the qualification chain at the outermost level of the .NET Framework class library, e.g.:

    Global.System.Int32

This is useful if you are in a situation where you have defined a namespace in your code nested in another namespace (e.g. **MyNamespace.System**) and you have a **System.Int32** declaration inside.
