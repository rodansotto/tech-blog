---
title: ".NET Framework: From 2.0 to 3.0, to 3.5, to 4.0, and finally to 4.5, what’s the difference?"
date: "2013-05-05"
categories: 
  - "net"
---

I thought it would be nice to know what the differences between these **.NET Framework** versions are.  I will not be discussing here the differences in versions of **ASP.NET** as this will be a topic on its own under the ASP.NET section.  Same with **C#**, it will be a topic on its own under the C# section.  Plus I won’t be discussing all the differences here, only the things that matter to me most.  So let’s start.

- **.NET Framework 3.0**
    1. The only update to this version (from **2.0**) is the inclusion of the following technologies:
    2. **Windows Communication Foundation (WCF)**.  Important to follow this technology if you are into developing service-oriented applications.
    3. **Windows Presentation Foundation (WPF)** .  If you are mostly developing web applications, you probably will not be needing this.
    4. **Windows Workflow Foundation (WF)**.
    5. **Windows Cardspace**.
    6. **.NET Framework 3.0** did not come with any version of Visual Studio.  But **.NET Framework 2.0** did and it came with **Visual Studio 2005**
- **.NET Framework 3.5**
    
    1. The following are some of the features added:
    2. **Language-Integrated Query (LINQ)** which allows you to query .NET Framework collections, SQL Server databases, ADO.NET Datasets, and XML documents.
    3. **Workflow Services** which allow you to author **WCF** services using **WF** or expose existing **WF** workflow as a **WCF** service.
    4. **WCF REST Programming Model** which allows you to expose WCF web services through basic **HTTP** requests without requiring **SOAP**.
        - You can now easily work with syndication feeds in **Atom**, **RSS**, or other custom formats, if you’re into blogging applications.
        - With new support to **ASP.NET AJAX** and **Javascript Object Notation (JSON)** data format, you can now expose operations from a WCF service to AJAX clients.
        - So what is **REST** and **JSON**?
        - **REST** which stands for **Representational State Transfer** is basically an architectural style attributed to a distributed system, like the **World Wide Web**, consisting of clients and servers, dealing with requests and responses revolving around resources.
        - **JSON** is an alternative to **XML** for sending data over a network connection that is also text-based like XML but derived from the **Javascript** language.  It would look something like this:
    
    {
        "firstName": "John",
        "lastName": "Smith",
        "age": 25,
        "address": {
            "streetAddress": "21 2nd Street",
            "city": "New York",
            "state": "NY",
            "postalCode": 10021
        },
        "phoneNumbers": \[
            {
                "type": "home",
                "number": "212 555-1234"
            },
            {
                "type": "fax",
                "number": "646 555-4567"
            }
        \]
    }
    
    1. **Peer-to-Peer Networking** which allows you to share and collaborate between several network devices without using any server.
    2. **ADO.NET Entity Framework** which allows you to work with data in a much higher level of abstraction without having to concern with tables and columns, thus reducing code required to create and maintain data-oriented applications.
    3. **.NET Framework 3.5** was released with **Visual Studio 2008**.
    4. For a complete list of what's new in 3.5, go to this [link](http://msdn.microsoft.com/en-us/library/bb332048(v=vs.90).aspx).
- **.NET Framework 4.0**
    1. The following are what’s new in this version:
    2. **In-Process Side-by-Side Execution** which allows you in your application to load and start multiple versions of .NET Framework in the same process.
    3. **Application Domain Diagnostics and Performance Monitoring** which allows you to monitor all application domains in the process, not just the process itself.
    4. **Parallel Computing** which allows you to write efficient, fine-grained, and scalable parallel code in a natural idiom without having to work directly with threads and thread pool.
    5. The rest of the changes are mostly improvements on .NET Framework 3.5.
    6. **.NET Framework 4.0** was released with **Visual Studio 2010**.
    7. For a complete list of what's new in 4.0, go to this [link](http://msdn.microsoft.com/en-us/library/vstudio/ms171868(v=vs.100).aspx).
- **.NET Framework 4.5**
    1. Some of the features added are:
    2. **.NET for Windows Store apps** which allows you to build Windows Store apps for Windows.
    3. **Portable Class Libraries** which allow you to build assemblies that can work without code modification on multiple platforms like **Windows 7**, **Windows 8**, **Silverlight**, **Windows Phone**, and **XBox 360**.
    4. The rest of the changes are mostly improvements on .NET Framework 4.0.
    5. **.NET Framework 4.5** was released with **Visual Studio 2012**.
    6. For a complete list of what's new in 4.5, go to this [link](http://msdn.microsoft.com/en-us/library/ms171868.aspx).
