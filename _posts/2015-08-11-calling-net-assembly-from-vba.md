---
title: "Calling .Net Assembly from VBA"
date: "2015-08-11"
categories: 
  - "net"
  - "ms-access"
---

Stuck in VBA?  You don’t have to be.  You can move all your business logic code from VBA to a .Net assembly.  It’s easier than you might think and this post will show you how.

First you need to create a new _Class Library_ project and below is the basic structure of a _COM-callable wrapper_ for your .Net assembly.

\[code language="csharp" light="true"\] // need this so we can decorate our classes with ClassInterface // and ComVisible attributes using System.Runtime.InteropServices;

// namespace should be the same as assembly name // so when VBA calls it via New or CreateObject() it will use same reference name // and prog ID // ie. New YourNetAssembly.TestFunc or CreateObject("YourNetAssembly.TestFunc") namespace YourNetAssembly { // need to decorate class with following attributes // so we can access its members using intellisense in VBA editor \[ClassInterface(ClassInterfaceType.AutoDual), ComVisible(true)\] public class TestFunc { public int Add(int num1, int num2) { return num1 + num2; } } } \[/code\]

 

And when you are ready to compile or build, the next thing you need to do is check the _Make assembly COM-Visible_ in your project’s _Properties –> Application –> Assembly Information…_.

Now if you are developing your VBA application (be it MS Access or MS Excel) locally or on the same computer where you build your .Net assembly, you can have Visual Studio register your COM automatically by checking the _Register for COM interop_ in your project’s _Properties –> Build_.

But if you are developing your VBA application remotely or on a different computer, then you will need to copy your .Net assembly to that computer and manually register it using _regasm.exe_.  You might want to create a batch file containing the following command so you don’t have to type it every time.

`c:\Windows\Microsoft.NET\Framework\v4.0.30319\regasm.exe YourNetAssembly.dll /codebase /tlb`

Note the correct .Net Framework version that your .Net assembly is created in.  Each version of the .Net Framework will have its own folder.  Also this command is run from the VBA application folder where the .Net assembly resides.  Yours might have a different setup so take note.

_/codebase_ option adds the .Net assembly’s path on the disk to the Windows registry.  _/tlb_ option generates the type library and saves it on the same folder as your .Net assembly.

Note that you need administrator privileges on the computer to generate a type library, be it via Visual Studio or regasm.exe.  If you already have an administrator privilege, you need to open Visual Studio or the command prompt as admin by right-clicking and selecting _Run as administrator_.

Once registered, you then add a reference to it from your VBA application.  From the VBA editor, go to _Tools –> References…_ and look for your .Net assembly in the list of _Available References_.  Its name should be the assembly name.  You can check the assembly name in your project’s _Properties –> Application_ under _Assembly name_.  Once added, you can now start calling your .Net assembly from VBA.

There are two ways you might want to call your .Net assembly.  Using the _New_ keyword, or using _CreateObject()_.

\[code language="vb" light="true"\] Dim objTestFunc As New YourNetAssembly.TestFunc ' OR ... Dim objTestFunc As Object Set objTestFunc = CreateObject("YourNetAssembly.TestFunc")

Dim intResult As Integer intResult = objTestFunc.Add(1, 2) MsgBox intResult \[/code\]

 

Great, but how about debugging or stepping into the .Net assembly?  Well if you have both Visual Studio and VBA development environments on one machine, then it would be easier.  You just set a breakpoint inside your .Net assembly in Visual Studio.  Then in your project’s _Properties –> Debug_, enter the full pathname to the program that runs your VBA application (maybe MS Access or MS Excel) in _Start external program_.  Then in the _Command line arguments_, enter the full pathname to your VBA application.  Save changes then press F5 to run.  This will run MS Access or MS Excel (whichever one you are using) which in turn runs your VBA application.  When your VBA application calls your .Net assembly, it will break into the Visual Studio debugging environment.

What about if your VBA development environment is on a different machine?  Well hope is not lost yet.  Assuming you have a debugger program installed on that machine, you can place a _Debug.Assert(false);_ or _Debugger.Break();_ in your .Net assembly and this will force it to go into debugging mode when it hits that code and open the debugger program.  Be sure to copy the PDB (debug) file for your .Net assembly plus the source code so you can step through .Net code.

\[code language="csharp" light="true"\] public int Add(int num1, int num2) { System.Diagnostics.Debugger.Break(); // OR ... System.Diagnostics.Debug.Assert(false);

// if Debugger.Break() does not work properly i.e. it does not return back // to the VBA application after debugging, // then use Debug.Assert(false) instead

return num1 + num2; } \[/code\]

 

So that’s all there is to it.  Easy eh?  So start coding away then!

**EDIT:**

Actually you don't need to check the _Make assembly COM-Visible_ in your project’s _Properties –> Application –> Assembly Information…_. unless you want to expose all your public classes in the assembly.  And besides since you still need to decorate your public classes with COM attributes, might as well just use COM attributes to select only those ones you want to be COM-visible.

I found this great article that summarizes what you need to do: [Best Practice in Writing a COM-Visible Assembly (C#)](http://www.codeproject.com/Articles/612604/Best-Practice-in-Writing-a-COM-Visible-Assembly-Cs).  I didn't bother adding the _ProgId_ attribute to my COM-visible classes though, but the rest I did.  Plus I created an interface for each, as was suggested in the article.  Nice thing having an interface is you can control which methods in your COM-visible classes you want to expose, giving you a more granular level of control. ![]({{ site.baseurl }}/assets/images/vbalogo.png)


