---
title: ".NET 2.0: Notes on Foundation Part 4 (C#)"
date: "2009-04-03"
categories: 
  - "net"
---

**Collections**

Under **System.Collections** namespace are the following collections: **ArrayList**, **SortedList**, **Queue**, **Stack**, **Hashtable**, **BitArray**, **StringCollection**, **StringDictionary**, **ListDictionary**, **HybridDictionary**, and **NameValueCollection**.

**ArrayList**

**ArrayList** is the most basic of all collections.  It is a simple resizeable, index-based collections of objects.

<table border="0" cellspacing="0" cellpadding="0" width="630"><tbody><tr><td valign="top" width="628"><font size="2" face="Courier New">ArrayList arrayList = <span style="color:#0000ff;">new</span> ArrayList();<br><br><span style="color:#008000;">// add individual items</span><br><span style="color:#0000ff;">string</span> s = <span style="color:#006080;">"Hello"</span>;<br>arrayList.Add(s);<br>arrayList.Add(<span style="color:#006080;">"World!!!"</span>);<br>arrayList.Add(100);<br>arrayList.Add(<span style="color:#0000ff;">new</span> <span style="color:#0000ff;">object</span>());<br><br><span style="color:#008000;">// add multiple items</span><br><span style="color:#0000ff;">string</span>[] anArray = <span style="color:#0000ff;">new</span> <span style="color:#0000ff;">string</span>[] { <span style="color:#006080;">"less"</span>, <span style="color:#006080;">"is"</span>, <span style="color:#006080;">"more"</span> };<br>arrayList.AddRange(anArray);<br><span style="color:#0000ff;">object</span>[] anotherArray = <span style="color:#0000ff;">new</span> <span style="color:#0000ff;">object</span>[] { <span style="color:#0000ff;">new</span> <span style="color:#0000ff;">object</span>(), <span style="color:#0000ff;">new</span> ArrayList() };<br>arrayList.AddRange(anotherArray);<br><br><span style="color:#008000;">// insert item at specific position</span><br>arrayList.Insert(3, <span style="color:#006080;">"Hi All"</span>);<br><br><span style="color:#008000;">// insert multiple items at specific position</span><br><span style="color:#0000ff;">string</span>[] moreStrings = <span style="color:#0000ff;">new</span> <span style="color:#0000ff;">string</span>[] { <span style="color:#006080;">"good morning"</span>, <span style="color:#006080;">"nice to meet you"</span> };<br>arrayList.InsertRange(4, moreStrings);<br><br><span style="color:#008000;">// using indexer to set specific item</span><br>arrayList[3] = <span style="color:#006080;">"Hi All"</span>;<br><br><span style="color:#008000;">// remove item</span><br>arrayList.Add(<span style="color:#006080;">"Hello"</span>);<br>arrayList.Remove(<span style="color:#006080;">"Hello"</span>);<br><br><span style="color:#008000;">// remove first item in ArrayList</span><br>arrayList.RemoveAt(0);<br><br><span style="color:#008000;">// remove first four items in ArrayList</span><br>arrayList.RemoveRange(0, 4);<br><br><span style="color:#008000;">// using Contains(), IndexOf(), and Clear() methods</span><br><span style="color:#0000ff;">string</span> myString = <span style="color:#006080;">"My String"</span>;<br><span style="color:#0000ff;">if</span> (arrayList.Contains(myString))<br>{<br><span style="color:#0000ff;">&nbsp; int</span> index = arrayList.IndexOf(myString);<br>&nbsp; arrayList.RemoveAt(index);<br>}<br><span style="color:#0000ff;">else</span><br>{<br>&nbsp; arrayList.Clear();<br>}</font></td></tr></tbody></table>

**Iterating Over Items In Collections**

To iterate items in a collection such as the **ArrayList**, you can use either the **for** loop, **IEnumerator** interface, or the **foreach** loop.

<table border="0" cellspacing="0" cellpadding="0" width="630"><tbody><tr><td valign="top" width="628"><font size="2"><font face="Courier New"><span style="color:#008000;">// using for loop</span><br><span style="color:#0000ff;">for</span> (<span style="color:#0000ff;">int</span> i = 0; i &lt; coll.Count; ++i)<br>{<br>&nbsp; Console.WriteLine(coll[i]);<br>}<br><br><span style="color:#008000;">// using IEnumerator interface</span><br>IEnumerator enumerator = coll.GetEnumerator();<br><span style="color:#0000ff;">while</span> (enumerator.MoveNext())<br>{<br>&nbsp; Console.WriteLine(enumerator.Current);<br>}<br><br><span style="color:#008000;">// using foreach loop</span><br><span style="color:#0000ff;">foreach</span> (<span style="color:#0000ff;">object</span> item <span style="color:#0000ff;">in</span> coll)<br>{<br>&nbsp; Console.WriteLine(item);<br>}</font></font></td></tr></tbody></table>

**Interfaces in Collections**

.NET supports the following interfaces that are implemented by collections: **IEnumerable**, **ICollection**, and **IList**. 

**IEnumerable** interface is used to provide a common way to iterate over a collection.  Its important properties and methods are: **Current**, **MoveNext()**, and **Reset()**.

**ICollection** is derived from **IEnumerable** and is used to provide a common way to get the items in the collection as well as to copy the collection to an **Array** object.  Its important properties and methods are: **Count**, and **CopyTo()**.

**IList** is derived from **ICollection** and is used to provide a common way to expose lists of items.  Its important properties and methods are: **Item**, **Add()**, **Clear()**, **Contains()**, **IndexOf()**, **Insert()**, **Remove()**, and **RemoveAt()**.

**Sorting Items In Collections**

To sort items in an **ArrayList**, you use the **Sort()** method.  The **Sort()** method uses the **Comparer** class which is a default implementation that supports the **IComparer** interface.

To specify an **IComparer** object to use instead of the default, you use the overloaded **Sort()** method that takes in an **IComparer** object.

<table border="0" cellspacing="0" cellpadding="0" width="400"><tbody><tr><td valign="top" width="400"><font size="2" face="Courier New">coll.Sort(<span style="color:#0000ff;">new</span> CaseInsensitiveComparer());</font></td></tr></tbody></table>

You can also write your own comparer by implementing the **Compare()** method of the **IComparer** interface.

<table border="0" cellspacing="0" cellpadding="0" width="630"><tbody><tr><td valign="top" width="628"><font size="2"><font face="Courier New"><span style="color:#0000ff;">public</span> <span style="color:#0000ff;">class</span> DescendingComparer : IComparer<br>{<br>&nbsp; CaseInsensitiveComparer _comparer = <span style="color:#0000ff;">new</span> CaseInsensitiveComparer();<br><br><span style="color:#0000ff;">&nbsp; public</span> <span style="color:#0000ff;">int</span> Compare(<span style="color:#0000ff;">object</span> x, <span style="color:#0000ff;">object</span> y)<br>&nbsp; {<br><span style="color:#008000;">&nbsp;&nbsp;&nbsp; // reversing the compared objects to get descending comparisons</span><br><span style="color:#0000ff;">&nbsp;&nbsp;&nbsp; return</span> _comparer.Compare(y, x);<br>&nbsp; }<br>}<br><br>coll.Sort(<span style="color:#0000ff;">new</span> DescendingComparer());</font></font></td></tr></tbody></table>
