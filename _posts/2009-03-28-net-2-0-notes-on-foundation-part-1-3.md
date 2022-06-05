---
title: ".NET 2.0: Notes on Foundation Part 1"
date: "2009-03-28"
categories: 
  - "net"
---

**Nullable Type**

In .NET 2.0, you can declare a variable as **Nullable**:

<table border="0" cellspacing="0" cellpadding="0" width="400"><tbody><tr><td valign="top" width="400"><font size="2" face="Courier New">Nullable&lt;<span style="color:#0000ff;">bool</span>&gt; b = <span style="color:#0000ff;">null</span>;<br><br><span style="color:#008000;">// shorthand notation</span><br><span style="color:#0000ff;">bool</span>? b = <span style="color:#0000ff;">null</span>;</font></td></tr></tbody></table>

**String versus StringBuilder**

Strings are immutable in .NET.  If you want to combine multiple strings, you can use **String** class’s **Concat**, **Join**, or **Format** methods or use **StringBuilder** class.

**Arrays**

To declare, initialize and sort an array:

<table border="0" cellspacing="0" cellpadding="0" width="630"><tbody><tr><td valign="top" width="628"><font size="2"><font face="Courier New"><span style="color:#008000;">// Declare and initialize an array.</span><br><span style="color:#0000ff;">int</span>[] arr = { 3, 1, 2 };<br><br><span style="color:#008000;">// Call a shared/static array method.</span><br>Array.Sort(arr);<br><br><span style="color:#008000;">// Display the result.</span><br>Console.WriteLine(<span style="color:#006080;">"{0}, {1}, {2}"</span>, arr[0], arr[1], arr[2]);</font></font></td></tr></tbody></table>

**Try/Catch/Finally Blocks**

Use multiple **Catch** blocks to filter exceptions, ordered from most specific to least specific.  Make sure variables you want to access in the **Finally** block is declared outside of the **Try** block.  You can also use nested  **Try/Catch/Finally** blocks.

**Commonly Used Interfaces**

**IComparable**, **IDisposable**, **IConvertible**, **ICloneable**, **IEquatable**, and **IFormattble** are commonly used interfaces.

**Generics**

To declare a generic type:

<table border="0" cellspacing="0" cellpadding="0" width="400"><tbody><tr><td valign="top" width="400"><font size="2"><font face="Courier New"><span style="color:#0000ff;">class</span> Gen&lt;T, U&gt;<br>{<br><span style="color:#0000ff;">&nbsp; public</span> T t;<br><span style="color:#0000ff;">&nbsp; public</span> U u;<br><br><span style="color:#0000ff;">&nbsp; public</span> Gen(T _t, U _u)<br>&nbsp; {<br>&nbsp;&nbsp;&nbsp; t = _t;<br>&nbsp;&nbsp;&nbsp; u = _u;<br>&nbsp; }<br>}</font></font></td></tr></tbody></table>

To consume a generic type:

<table border="0" cellspacing="0" cellpadding="0" width="630"><tbody><tr><td valign="top" width="628"><font size="2"><font face="Courier New"><span style="color:#008000;">// Add two strings using the Gen class</span><br>Gen&lt;<span style="color:#0000ff;">string</span>, <span style="color:#0000ff;">string</span>&gt; ga = <span style="color:#0000ff;">new</span> Gen&lt;<span style="color:#0000ff;">string</span>, <span style="color:#0000ff;">string</span>&gt;(<span style="color:#006080;">"Hello, "</span>, <span style="color:#006080;">"World!"</span>);<br>Console.WriteLine(ga.t + ga.u);<br><br><span style="color:#008000;">// Add a double and an int using the Gen class</span><br>Gen&lt;<span style="color:#0000ff;">double</span>, <span style="color:#0000ff;">int</span>&gt; gb = <span style="color:#0000ff;">new</span> Gen&lt;<span style="color:#0000ff;">double</span>, <span style="color:#0000ff;">int</span>&gt;(10.125, 2005);<br>Console.WriteLine(gb.t + gb.u);</font></font></td></tr></tbody></table>

To use a constraint so that you are not limited to just the base **Object** class:

<table border="0" cellspacing="0" cellpadding="0" width="400"><tbody><tr><td valign="top" width="400"><font size="2"><font face="Courier New"><span style="color:#0000ff;">class</span> CompGen&lt;T&gt;<br><span style="color:#0000ff;">where</span> T : IComparable<br>{<br><span style="color:#0000ff;">&nbsp; public</span> T t1;<br><span style="color:#0000ff;">&nbsp; public</span> T t2;<br><br><span style="color:#0000ff;">&nbsp; public</span> CompGen(T _t1, T _t2)<br>&nbsp; {<br>&nbsp;&nbsp;&nbsp; t1 = _t1;<br>&nbsp;&nbsp;&nbsp; t2 = _t2;<br>&nbsp; }<br><br><span style="color:#0000ff;">&nbsp; public</span> T Max()<br>&nbsp; {<br><span style="color:#0000ff;">&nbsp;&nbsp;&nbsp; if</span> (t2.CompareTo(t1) &lt; 0)<br><span style="color:#0000ff;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; return</span> t1;<br><span style="color:#0000ff;">&nbsp;&nbsp;&nbsp; else</span><br><span style="color:#0000ff;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; return</span> t2;<br>&nbsp; }<br>}</font></font></td></tr></tbody></table>

Besides an **interface**, you can also use a **base class**, a **constructor** or a **reference or value type** for your constraints.
