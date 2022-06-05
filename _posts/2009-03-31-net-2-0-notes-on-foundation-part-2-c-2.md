---
title: ".NET 2.0: Notes on Foundation Part 2 (C#)"
date: "2009-03-31"
categories: 
  - "net"
---

**Explicit Conversion**

The following are methods for explicit conversion: **System.Convert**, **(type)** cast operator, type.**ToString**, type.**Parse**, type.**TryParse**, and type.**TryParseExact**.

**Conversion in Custom Types**

The following are ways to provide conversion for your own types: conversion operators (which are new to .NET 2.0), **ToString** and **Parse** overrides, **System.IConvertible** implementation, and **TypeConverter** class implementation.

**File System Classes**

There are 2 types of these classes: informational and utility.  Informational classes are **FileInfo** and **DirectoryInfo**, both derived from **FileSystemInfo**.  **DriveInfo** is also an informational class but not derived from **FileSystemInfo**.  Utility classes are **File**, **Directory**, and **Path** (which is  a useful class for parsing file system paths).

There is also this **FileSystemWatcher** class which provides methods for monitoring file system directories for changes.

**Reading and Writing Files**

The **Stream** class is an abstract class from which the following classes are derived from: **FileStream**, **MemoryStream**, **CryptoStream**, **NetworkStream**, and **GZipStream**.

To start a read or write operation on a file stream, you begin with the **File** class.  It can return a **FileStream**, **StreamReader**, or **StreamWriter** object.

<table border="0" cellspacing="0" cellpadding="0" width="630"><tbody><tr><td valign="top" width="628"><font size="2"><font face="Courier New"><span style="color:#008000;">// returns a FileStream object</span><br></font><font face="Courier New"><font size="1">FileStream readFile = File.Open(<span style="color:#006080;">@"C:\boot.ini"</span>, FileMode.Open, FileAccess.Read);<br></font>FileStream writeFile = File.Create(<span style="color:#006080;">@"c:\myfile.txt"</span>);<br><br><span style="color:#008000;">// returns a StreamReader object</span><br>StreamReader reader = File.OpenText(<span style="color:#006080;">@"C:\boot.ini"</span>);<br><br><span style="color:#008000;">// returns a StreamWriter object</span><br>StreamWriter writer = File.CreateText(<span style="color:#006080;">@"c:\myfile.txt"</span>);<br><br><span style="color:#008000;">// reads the entire file</span><br>Console.WriteLine(File.ReadAllText(<span style="color:#006080;">@"C:\boot.ini"</span>));<br><br><span style="color:#008000;">// writes string to new file</span><br>File.WriteAllText(<span style="color:#006080;">@"c:\myfile.txt"</span>, <span style="color:#006080;">"Hello World!!!"</span>);</font></font></td></tr></tbody></table>

Do not confuse the **File** class with the **FileInfo** class.  The **FileInfo** class does not have the capability to work with file streams.  **Directory** class is also provided just like there is a **DirectoryInfo** class.

**Reader and Writers**

The **StreamReader** and **StreamWriter** classes are derived from **TextReader** and **TextWriter** abstract classes, respectively.  All text-based readers and writers are all derived from these abstract classes.  One example is the **StringReader** and **StringWriter** pair.  There is also a reader and writer pair for reading and writing binary data, the **BinaryReader** and **BinaryWriter**.

**MemoryStream and BufferedStream**

**MemoryStream** class is commonly used to temporarily store data in memory before storing it to a more permanent area, such as a file.

<table border="0" cellspacing="0" cellpadding="0" width="400"><tbody><tr><td valign="top" width="400"><font size="2"><font face="Courier New"><span style="color:#008000;">// Create an instance of MemoryStream</span><br>MemoryStream memStrm = <span style="color:#0000ff;">new</span> MemoryStream();<br><br><span style="color:#008000;">// Use StreamWriter to write to the MemoryStream</span><br>StreamWriter writer = <span style="color:#0000ff;">new</span> StreamWriter(memStrm);<br>writer.WriteLine(<span style="color:#006080;">"Hello"</span>);<br>writer.WriteLine(<span style="color:#006080;">"World!!!"</span>);<br><br><span style="color:#008000;">// Force the writer to push the data into the underlying stream</span><br>writer.Flush();<br><br><span style="color:#008000;">// Create a file stream</span><br>FileStream fileStrm = File.Create(<span style="color:#006080;">@"c:\myfile.txt"</span>);<br><br><span style="color:#008000;">// Write the entire Memory stream to the file</span><br>memStrm.WriteTo(fileStrm);<br><br><span style="color:#008000;">// Clean up</span><br>writer.Close();<br>fileStrm.Close();<br>memStrm.Close();</font></font></td></tr></tbody></table>

**BufferedStream** class is used to buffer reads and writes through the stream that it wraps.  The code example above for **MemoryStream** can be rewritten to use the **BufferedStream**.

<table border="0" cellspacing="0" cellpadding="0" width="630"><tbody><tr><td valign="top" width="628"><font size="2" face="Courier New">FileStream fileStrm = File.Create(<span style="color:#006080;">@"c:\myfile.txt"</span>);<br>BufferedStream bufferedStrm = <span style="color:#0000ff;">new</span> BufferedStream(fileStrm);<br>StreamWriter writer = <span style="color:#0000ff;">new</span> StreamWriter(bufferedStrm);<br>writer.WriteLine(<span style="color:#006080;">"Hello World!!!"</span>);<br>writer.Close();</font></td></tr></tbody></table>

**Compression Streams**

Two classes you use for compression and decompression: **GZipStream** and **DeflateStream**.  If you plan on using the compressed file with **gzip** tool, then use **GZipStream**.  Otherwise use **DeflateStream** which produces slightly smaller files.
