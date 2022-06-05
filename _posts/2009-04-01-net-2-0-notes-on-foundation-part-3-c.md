---
title: ".NET 2.0: Notes on Foundation Part 3 (C#)"
date: "2009-04-01"
categories: 
  - "net"
---

**Isolated Storage**

You use isolated storage in your .NET application if you want to save information on a hard drive without using a database or other means and still have safe access to it - meaning no need to worry if application has enough rights to do so.

To create a store, use **IsolatedStorageFile** class, which is responsible for creating files and folders in isolated storage.  You first need to scope the data you want in the store, that is, if you like your data to be specific to the calling assembly and the local machine, or specific to the calling assembly and the current user.

<table border="0" cellspacing="0" cellpadding="0" width="630"><tbody><tr><td valign="top" width="628"><font size="2"><font face="Courier New"><span style="color:#008000;">// specific to assembly and local machine</span><br>IsolatedStorageFile machineStore =<br>IsolatedStorageFile.GetMachineStoreForAssembly();<br><br><span style="color:#008000;">// specific to assembly and current user</span><br><font size="1">IsolatedStorageFile userStore = IsolatedStorageFile.GetUserStoreForAssembly();</font></font></font></td></tr></tbody></table>

To work with files in the store, use **IsolatedStorageFileStream** class, which derives from **FileStream** class.

<table border="0" cellspacing="0" cellpadding="0" width="630"><tbody><tr><td valign="top" width="628"><font size="2"><font face="Courier New"><font size="1"><font size="2">IsolatedStorageFileStream userStream =<br></font><span style="color:#0000ff;">&nbsp; new</span> IsolatedStorageFileStream(<span style="color:#006080;">"UserSettings.set"</span>, FileMode.Create, userStore);</font><br>StreamWriter userWriter = <span style="color:#0000ff;">new</span> StreamWriter(userStream);<br>userWriter.WriteLine(<span style="color:#006080;">"User Prefs"</span>);<br>userWriter.Close();<br><br>IsolatedStorageFileStream userStream =<br><span style="color:#0000ff;">&nbsp; <font size="1">new</font></span><font size="1"> IsolatedStorageFileStream(<span style="color:#006080;">"UserSettings.set"</span>, FileMode.Open, userStore);</font><br><span style="color:#0000ff;">string</span>[] files = userStore.GetFileNames(<span style="color:#006080;">"UserSettings.set"</span>);<br><span style="color:#0000ff;">if</span> (files.Length == 0)<br>{<br>&nbsp; Console.WriteLine(<span style="color:#006080;">"No data saved for this user"</span>);<br>}<br><span style="color:#0000ff;">else</span><br>{<br><span style="color:#008000;">&nbsp; // ...</span><br>}</font></font></td></tr></tbody></table>

You can also work with directories using the methods found in the **IsolatedStorageFile** class, such as **CreateDirectory()** and **GetDirectoryNames()**.

Last important point in using isolated storage is that you have to explicitly permission your code to access it by annotating your class or method with the **IsolatedStorageFilePermission** class.

<table border="0" cellspacing="0" cellpadding="0" width="630"><tbody><tr><td valign="top" width="628"><font size="2" face="Courier New">[IsolatedStorageFilePermission(SecurityAction.Demand,<br>&nbsp; UserQuota=1024,<br>&nbsp; UsageAllowed=IsolatedStorageContainment.AssemblyIsolationByUser)]<br><span style="color:#0000ff;">class</span> MyClass<br>{<br><span style="color:#008000;">// ...</span><br>}</font></td></tr></tbody></table>

**Regular Expressions**

To use regular expressions in your application, you use **System.Text.RegularExpressions.Regex** class.

<table border="0" cellspacing="0" cellpadding="0" width="630"><tbody><tr><td valign="top" width="628"><font size="2"><font face="Courier New"><span style="color:#008000;">// checks if input string matches regular expression</span><br><span style="color:#0000ff;">if</span> (Regex.IsMatch(regexString, inputString)<br>&nbsp; Console.WriteLine(<span style="color:#006080;">"Input matches regular expression."</span>);<br><span style="color:#0000ff;">else</span><br>&nbsp; Console.WriteLine(<span style="color:#006080;">"Input DOES NOT match regular expression."</span>);<br><br><span style="color:#008000;">// extracts matched data</span><br><span style="color:#0000ff;">string</span> inputString = <span style="color:#006080;">"Company Name: MyCompany, Inc."</span>;<br>Match m = Regex.Match(inputString, <span style="color:#006080;">@"Company Name: (.*$)"</span>);<br>Console.WriteLine(m.Groups[1]);<br><br><span style="color:#008000;">// reformats extracted substring</span><br>Regex r = <span style="color:#0000ff;">new</span> Regex(<span style="color:#006080;">@"^(?&lt;proto&gt;\w+)://[^/]+?(?&lt;port&gt;:\d+)?/"</span>,<br>RegexOptions.Compiled);<br>Console.WriteLine(r.Match(urlString).Result(<span style="color:#006080;">"${proto}${port}"</span>));<br><br><span style="color:#008000;">// replaces substring</span><br><span style="color:#008000;">// in this example, it replaces mm/dd/yy with dd-mm-yy</span><br>Console.WriteLine(Regex.Replace(inputString,<br><span style="color:#006080;">&nbsp; "\\b(?&lt;month&gt;\\d{1,2})/(?&lt;day&gt;\\d{1,2})/(?&lt;year&gt;\\d{2,4})\\b"</span>,<br><span style="color:#006080;">&nbsp; "${day}-${month}-${year}"</span>));</font></font></td></tr></tbody></table>

For quick help on how to form regular expressions go to this [link](http://www.addedbytes.com/download/regular-expressions-cheat-sheet-v2/pdf/), which is a cheat sheet by the way.

**Encoding and Decoding**

To work with encodings, use the **System.Text.Encoding** class.

<table border="0" cellspacing="0" cellpadding="0" width="630"><tbody><tr><td valign="top" width="628"><p><font size="2"><font face="Courier New"><span style="color:#008000;">// converts from one code page to another</span><br><span style="color:#008000;">// get Korean encoding</span><br>Encoding e = Encoding.GetEncoding(<span style="color:#006080;">"Korean"</span>);<br><span style="color:#008000;">// convert ASCII bytes to Korean encoding</span><br><span style="color:#0000ff;">byte</span>[] encoded;<br>encoded = e.GetBytes(<span style="color:#006080;">"Hello, world!"</span>);<br><span style="color:#008000;">// display the byte codes</span><br><span style="color:#0000ff;">for</span> (<span style="color:#0000ff;">int</span> i = 0; i &lt; encoded.Length; i++)<br>&nbsp; Console.WriteLine(<span style="color:#006080;">"Byte {0}: {1}"</span>, i, encoded[i]);<br><br><span style="color:#008000;">// examines supported code pages</span><br>EncodingInfo[] eis = Encoding.GetEncodings();<br><span style="color:#0000ff;">foreach</span> (EncodingInfo ei <span style="color:#0000ff;">in</span> eis)<br>{<br>&nbsp; Console.WriteLine(<span style="color:#006080;">"{0}: {1}, {2}"</span>, ei.CodePage, ei.Name, ei.DisplayName);<br>}<br><br><span style="color:#008000;">// specifies encoding type when writing a file</span><br><font size="1">StreamWriter utf7Writer = <span style="color:#0000ff;">new</span> StreamWriter(<span style="color:#006080;">"utf7.txt"</span>, <span style="color:#0000ff;">false</span>, Encoding.UTF7);</font><br>utf7Writer.WriteLine(<span style="color:#006080;">"Hello World!!!"</span>);<br>utf7Writer.Close();<br><br><span style="color:#008000;">// specifies encoding type when reading a file</span><br>StreamReader utf7Reader = <span style="color:#0000ff;">new</span> StreamReader(<span style="color:#006080;">"utf7.txt"</span>, Encoding.UTF7);<br>Console.WriteLine(utf7Reader.ReadToEnd());<br>utf7Reader.Close();</font></font></p></td></tr></tbody></table>
