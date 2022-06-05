---
title: "VB 2005: Quick introduction to the world of .NET"
date: "2007-03-28"
categories: 
  - "vb-net"
---

Before **.NET** came, [**COM (Component Object Model)**](http://www.microsoft.com/com/default.mspx) was the norm.  You build COM objects to make your code reusable and so that you can fit them in a 3-tier or n-tier architecture.  This architecture was called or marketed by Microsoft as **DNA (Distributed interNet Architecture)**.  It is just a way to architect or build distributed business applications using (but not necessarily) Microsoft technologies.  One of its technologies besides COM, is **MTS** (**Microsoft Transaction Server**).  MTS is a run-time environment that provides objects with not only transaction services but also concurrency, resource pooling, security, context management, and other system-level services.  It provides location transparency as well.  Then there is this **COM+** which is just COM and MTS combined.

Now that we have .NET, it's time to learn this new technology from Microsoft which I think will stay with us for some time.  .NET is the next generation platform that developers can take advantage of in building not only distributed applications but the more traditional applications as well, more easily and intuitively.  Which is why .NET is appropriately called **[.NET Framework](http://msdn2.microsoft.com/en-us/netframework/default.aspx)**.

Here I am going to blog about .NET 2.0.  The latest version now is 3.0 but it is still relatively new and I think the knowledge you will get from understanding the .NET Framework even if it's not the latest version will be useful for a long time.

Basically the .NET Framework contains the following major components: **CLR (Common Language Runtime)**, **.NET Framework Base Classes**, **Windows Forms** and **ASP.NET**. 

**CLR** is where component loading, memory management, reference tracking for objects and garbage collection happens.  It includes a common system of datatypes and coupled with standard interface convention, provides cross-language inheritance.  It also provides easy deployment of your .NET applications. 

One thing to note about applications in .NET is that they are self-describing because **metadata**, the information that describes the applications, is stored together with the application itself.  This is key to the easy deployment in .NET.

**.NET Framework Base Classes** provides developers with a rich set of functionality (in classes and interfaces) that they can use to help them develop applications with lesser code.  These classes and interfaces are organized into namespaces.  Examples of popular namespaces would be **System.Collections**, **System.Data**, **System.Diagnostics**, **System.IO**, **System.Math**, **System.Reflection**, and **System.Security**.

**Windows Forms** is the user interface services provided by .NET Framework in building windows-based applications.  **Smart client** applications with rich user interface are now more practical under .NET, even for a large number of users.

**ASP.NET** is the part of .NET that provides services for developing web-based applications.  **Web Forms** and **Web Services** are part of ASP.NET.

**Web Forms** is used to develop browser-based user interfaces and much like in a standard Visual Basic form, code is separated from the layout and properties information of the user interface elements.  Before in classic ASP, code is all over the HTML page.

**Web Services** allows programs to talk to each other directly over the web using the **[SOAP (Simple Object Access Protocol)](http://www.w3.org/TR/soap12-part1/)** standard.  With web services, software functionality are exposed over the web as resources for building your distributed applications.

It is worth noting that ASP.NET 2.0 has been significantly improved from previous versions with more built-in functionality making it possible to write far less code.  Also ASP.NET components for user authentication are already prebuilt.

[**XML**](http://www.w3.org/XML/) is also at the center stage in the .NET Framework as most of the underlying technologies are dependent on XML.  It is used as a glue to tie pieces together internally and externally.

Some of the important changes in .NET 2.0 are the following: **partial classes** which allows coding for a class into multiple code modules; **generics** which allows generic collections to handle specific data types, declared when collection is created; **ClickOnce** which is a new technology for deploying across the web, with automatic updating; **My class** which provides easy access to most commonly used classes in .NET; **nullable types**; **operator overloading**; **IsNot** and **Using** keyword.
