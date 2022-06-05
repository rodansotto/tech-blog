---
title: "Access VBA: How To Call A Windows Form Application with Arguments"
date: "2014-01-17"
categories: 
  - "ms-access"
---

To call a Windows Form application (\*.exe) with arguments in VBA, you use the **[Shell()](http://office.microsoft.com/en-ca/access-help/shell-function-HA001228906.aspx)** function.

Shell "C:\\Dev\\SampleWinFormWithArgs.exe arg1", vbNormalFocus

 

Inside the Windows Form application, you get the command line arguments using **Environment.GetCommandLineArgs()**.

string\[\] args = Environment.GetCommandLineArgs();
// you can call GetCommandLineArgs() anytime, anywhere
foreach(string arg in args)
{
    // do stuff
    // note that the first argument string is the application pathname
}
