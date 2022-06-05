---
title: ".NET: Regular Expression Testers and Quick Reference Guides"
date: "2013-12-03"
categories: 
  - "net"
---

I talked briefly about regular expressions in .NET Framework [here](http://rodansotto.wordpress.com/?s=regular+expression#regex), how you can test for a match and how to extract or replace a matched group, or matched substring if you may.  The examples there used a named group to extract a matched group (e.g. **?<proto>**, **?<port>**, etc...).  It's worth mentioning that you can also extract a matched group using **$** (e.g. **$0**, **$1**, **$2**, ... **$n**, where **$0** is the whole string that was matched, **$1** is the first matched group, **$2**, the second matched group, and so on...).

Also it would be nice if you have a tool you can use to test out your regular expressions instead of testing it out in your code, compiling it, and running it.  Well there are tools out there available for you but the ones I liked the most are online tools and are listed below.

**Online Regular Expression Tester**

- [A Better .NET Regular Expression Tester](http://derekslager.com/blog/posts/2007/09/a-better-dotnet-regular-expression-tester.ashx) - it's user interface is not fancy but it does the job well.
- [Regex Storm .Net](http://regexstorm.net/tester) - this one is a much better user interface and does the job too.
- [RegExr](http://regexr.com/) - an online tool to learn, build, & test. It has a cheatsheet and a very good sample text to test your regex.

**Online Quick Reference Guides**

- [Regular Expressions Cheat Sheets](http://www.cheatography.com/davechild/cheat-sheets/regular-expressions/)
- [MSDN - Regular Expression Language - Quick Reference](http://msdn.microsoft.com/en-us/library/az24scfc(v=vs.100).aspx)
