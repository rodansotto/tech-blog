---
title: "VB 2005: Things to know about the Visual Studio 2005 IDE"
date: "2007-05-05"
categories: 
  - "vb-net"
---

When you first started your Visual Studio 2005 you were asked to specify the default settings and I set mine to **Visual Basic Development Settings**.  If you want to change this setting, say to **Visual C# Development Settings**, you need to go to **Tools -> Import and Export Settings...** and go through the wizard to change it.

When you go create a new project, one of the project templates that you can select is **Database**.  This project template lets you create classes that can run inside SQL Server 2005.  Note that there is another project template of the same name under the **Other Project Types** option.  They are not the same.

If you have used a previous Microsoft development tool (e.g. Visual Studio 6.0), you will notice that the **Solution Explorer** is similar to the project group, except that it can contain projects of any .NET language and may include database, testing, and installation projects as part of the overall solution.

Application settings are now stored in an XML file named **app.config** but when you create a new project, it does not create one by default.  Since this app.config file is stored in the application directory, you can run different versions of your application without encountering problems that you usually get if the settings were stored in the Windows Registry.

When you get to the **Assembly Information** screen (by double-clicking the **My Project** on the Solution Explorer and on the **Application** tab display, clicking the **Assembly Information...** button), you will notice the **GUID** attribute there.  The value of that attribute is used as the ID of the type library that will be created when the assembly is made visible to **COM** applications (the checkbox **Make assembly COM-Visible** is checked).

A new feature in the code window is outlining.  You will notice a **+** or **\-** sign on the left side of your code window.  This allows you to hide or show portions of your code.  If you don't like this feature you can disable it by selecting **Edit -> Outlining -> Stop Outlining**.  To bring outlining back, select **Edit -> Outlining -> Collapse to Definitions**. 

There is also this **#Region** directive that allows you to hide regions of code.  The code should be enclosed with **#Region** at top and **#End Region** at the end.  There should be a description after the **#Region** keyword which will be shown when this region of code is collapsed.  Example of code enclosed with the #Region directive:

>     #Region "My region of code"
>     Private Sub mySub()
>         ' ...
>     End Sub
>     #End Region

You'll notice in the Visual Studio 2005 IDE, that all the files that you are working on are in tabbed layout unlike in previous versions of Visual Studio, they are in MDI layout.  If you prefer the MDI layout, just go to **Tools -> Options** and under the **Environment -> General** category, on the **Window layout** section, select **Multiple documents**.

**Tools -> Options** is the place to customize your IDE.  It has customizations for your text editor like line numbering which if you turn it on will number all your lines of code.

You might also want to use the **Dynamic Help** feature in the IDE.  To show this window, select **Help -> Dynamic Help** or press **Ctrl+Alt+F4**.  This feature tries to guess what you are trying to do and shows a list of things that you might be interested in looking at.
