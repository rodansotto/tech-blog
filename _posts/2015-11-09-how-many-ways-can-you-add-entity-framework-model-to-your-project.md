---
title: "How Many Ways Can You Add Entity Framework Model To Your Project?"
date: "2015-11-09"
categories: 
  - "net"
---

![]({{ site.baseurl }}/assets/images/eflogo.png)

Let me count the ways.  3?  Well there are at least 3 ways you can add Entity Framework (EF) model to your .NET project, that I know of.  One is **Code First**, second is **Reverse Engineer Code First**, and third is the **ADO.NET Entity Data Model (EDMX)**.

**Code First**, as the name suggests, requires you to code your EF model.  Yep, this requires more coding but gives you  a lot more control.  Usually you go this route if you don’t have an existing database to model or you want to create a fresh new database for your project.  I have not tried this approach as mostly the projects I worked on already has existing database. 

In Code First, basically you create the classes that model your database,  optionally configure your classes using [Data Annotations](https://msdn.microsoft.com/en-ca/data/jj591583) (via class / property attributes) and/or [Fluent API](https://msdn.microsoft.com/en-ca/data/jj591617.aspx), and then create the database based on that model.  When you update the model, you can use [Code First Migrations](https://msdn.microsoft.com/en-us/data/jj591621.aspx) to update the database.  Microsoft’s [Code First to a New Database](https://msdn.microsoft.com/en-ca/data/jj193542.aspx) has a video and a step-by-step walkthrough on how to go about this approach.

**Reverse Engineer Code First** uses EF Power Tools to generate the code for you containing the [DbContext](https://msdn.microsoft.com/en-ca/data/jj729737.aspx) class, [POCO](https://en.wikipedia.org/wiki/Plain_Old_CLR_Object) classes, and Code First mapping classes, based on an existing database.  [EF Power Tools Summary of Commands](https://msdn.microsoft.com/en-us/data/jj593170.aspx) shows you a step-by-step walkthrough on how to do this plus some more, including customizing the default reverse engineer [T4 templates](https://msdn.microsoft.com/en-ca/library/bb126445(v=vs.110).aspx) and generating pre-compiled views to improve start-up performance. 

If you need to edit the t4 templates, I suggest getting a t4 editor such as [tangible T4 Editor](https://visualstudiogallery.msdn.microsoft.com/b0e2dde6-5408-42c2-bc92-ac36942bbee9) from the Visual Studio Gallery so you can get syntax highlighting at least.  When it comes to tweaking performance, [Performance Considerations for Entity Framework 4, 5, and 6](https://msdn.microsoft.com/en-us/data/hh949853) has some tips.  One way is to generate pre-compiled views.  [Pre-Generated Mapping Views](https://msdn.microsoft.com/en-us/data/dn469601.aspx) shows you how to do this using EF Power Tools and also via APIs provided in EF6 onwards.  [How to: Pre-Generate Views to Improve Query Performance](https://msdn.microsoft.com/en-us/library/vstudio/bb896240(v=vs.100).aspx) shows you how to generate pre-compiled views using EDM generator command line tool.

Code First and Reverse Engineer Code First does not automatically generate an **ADO.NET Entity Data Model (EDMX)** file.  Same goes too for EDMX, it does not automatically generate any code.  To generate the code you get from Code First in EDMX, you need to add a code generation item, basically download a t4 template and generate the code based on it.  [Database First](https://msdn.microsoft.com/en-us/data/jj206878.aspx) shows you how to create an EDMX from an existing database, view and edit it in EF Designer and generate the code.  [How to: Create a New .edmx File (Entity Data Model Tools)](https://msdn.microsoft.com/en-us/library/vstudio/cc716703(v=vs.100).aspx) has a section on adding EDMX from an existing database and contains tons of links to more information, definitely a good resource.

It can get confusing what these code first and database first mean.  It all lies down to how you synchronize your model changes between the database and code or more accurately where you make your model changes, is it in code or database?  Although in reverse engineer code first, you can change your model in the database, and re-generate the code, essentially doing a database first.




