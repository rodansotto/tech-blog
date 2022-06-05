---
title: "C#: Using or not using"
date: "2015-09-11"
categories: 
  - "c-sharp"
---

![]({{ site.baseurl }}/assets/images/csbloglogo21.png)



I am not referring to the **using** directive to import types defined in other namespaces, but I am referring to the **using** statement to define a scope where at the end of it an object will be disposed, such as this:

\[code language="csharp" light="true"\] using (var cn = new SqlConnection()) { // your code here... } \[/code\]

 

Just be aware that the **using** statement is just a shortcut or a convenient syntax for the below code:

\[code language="csharp" light="true"\] var cn = new SqlConnection(); try { // your code here... } finally { if (cn != null) ((IDisposable)cn).Dispose(); } \[/code\]

 

And if you have a **try**\-**catch** block in your method, either outside or inside the **using** statement, or maybe even both, then you need to make sure the flow of control and the logic when an exception occurs is what you would expect, because nested **try**\-**catch** block can become confusing.  Just remember the **using** statement is a **try**\-**finally** block.

My point is, don’t haphazardly use **using** statement especially if you are using it for several objects in your method, because depending on what you are trying to achieve, sometimes its better to just use a complete **try**\-**catch**\-**finally** block to make your code simpler to understand.

**EDIT:**

Rule of thumb is if the resource object you are trying to use in your method needs to be disposed of by your method then **using** statement is best.  And make sure you are instantiating the resource object inside the **using** statement and not outside and passing the variable to it.  See [using Statement (C# Reference)](https://msdn.microsoft.com/en-us/library/yh598w02(v=vs.100).aspx).
