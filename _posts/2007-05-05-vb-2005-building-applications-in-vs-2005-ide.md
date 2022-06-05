---
title: "VB 2005: Building applications in VS 2005 IDE"
date: "2007-05-05"
categories: 
  - "vb-net"
---

**Build Configurations**

New in VS 2005 IDE is the ability to choose which build configuration you want to use to build your applications.  You can create your own build configuration besides the **Debug** and **Release** build configuration that VS 2005 IDE already provides.

To choose which build configuration you want, you need to display the settings first by going to **Tools -> Options... -> Projects and Solutions -> General** and checking the **Show advanced build configurations** checkbox.  Then go to your project's properties by right-clicking your project and selecting **Properties** and clicking the **Compile** tab.  From there you can see the **Configuration** drop-down listbox where you can choose which build configuration you want and you can also change the settings associated to that build configuration like the **Build output path**, **Option explicit**, **Option strict**, etc.  You can also click the **Advanced Compile Options...** button for more advanced compiler settings.

To add a new build configuration or include/exclude projects from your build configuration if you are working on a solution with multiple projects, go to the  **Build** menu and select **Configuration** **Manager...**.

**Building and Debugging Applications**

To build your application, you can use **Build** or **Rebuild** just like in the old versions of Visual Studio.  During debugging, you have the **Output**, **Call Stack**, **Breakpoints**, **Locals**, and **Watch** windows to use to help you in your debugging efforts.  There is this another window, the **Autos** window, that automatically displays the variables used in the statement currently being executed and the statement just before it.

**Other Useful Features**

**Task List** not only tracks errors when building your applications but you can also use this to keep track of your **TODO** comments in your source code and user-entered tasks as well.  To be able to track comments in your source code, you need to create a standard comment with the apostrophe and begin your comment with **TODO**, just like this:

    ' TODO: Put your code here...

Then on your Task List window, if you double-click a comment task, you will be directed to the source code where the comment is, pretty neat huh?  You can open your Task List window by going to **View -> Other Windows -> Task List**.

The **Command** window is useful especially if it's in **immediate** mode.  It is like the **Immediate** window we are used to in Visual Basic 6.  The immediate mode is accessed by typing **immed** in the command prompt **\>** and pressing ENTER.  To return to the command mode, type **cmd** and press ENTER.

**Server Explorer**, as the name suggests, explores resources available on the server.  By default it inspects resources on the local machine.  You can also add a server for the Server Explorer to inspect.  Resources like **SQL Server databases**, **event logs**, **registry**, and **message queues** are just among the resources inspected by Server Explorer.

**Macros**

If you have programmed in Excel and used it's macro recording facility, you will find it similar in Visual Studio 2005 as well.  You start recording by going to **Tools -> Macros -> Record TemporaryMacro**.  A floating toolbar will appear to let you pause, stop, or cancel your recording.  Once finished you can view or edit your macro by going to **Tools -> Macros -> Macro Explorer**.  Now why would you want to use a macro?  Well this is useful if you have a code that you use frequently and by using a macro it can save you from typing the code.  Plus you can transfer the macro-generated code to a Visual Studio Add-In project so you can share it with others.  Another one of those cool features.
