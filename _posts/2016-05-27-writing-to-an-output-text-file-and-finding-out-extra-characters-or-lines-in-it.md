---
title: "Writing to an output text file and finding out extra characters or lines in it?"
date: "2016-05-27"
categories: 
  - "net"
---

If you're using File.OpenWrite() to create the output file, make sure the output file does not exist.  This [MSDN article](https://msdn.microsoft.com/en-us/library/system.io.file.openwrite(v=vs.110).aspx) explains what happens if output file exists:

> For an existing file, it does not append the new text to the existing text. Instead, it overwrites the existing characters with the new characters. If you overwrite a longer string (such as “This is a test of the OpenWrite method”) with a shorter string (such as “Second run”), the file will contain a mix of the strings (“Second runtest of the OpenWrite method”).
