---
title: "ASP.NET: Beginner's Resource on MVC 4, Entity Framework, and Razor"
date: "2013-11-12"
categories: 
  - "asp-net-mvc"
---

New to MVC 4/Entity Framework/Razor?  Then here are some links that are useful:

- [Getting Started with EF 5 using MVC 4 Tutorial](http://www.asp.net/mvc/tutorials/getting-started-with-ef-5-using-mvc-4)
- The tutorial above uses Code First to a New Database, meaning you create the EF model classes and generate the database.  But if you have an existing database, you can use [Code First to an Existing Database](http://msdn.microsoft.com/en-us/data/jj200620).
- For a quick introduction on the new view engine in MVC called Razor, visit [Scott Guthrie's blog posts on Razor](http://weblogs.asp.net/scottgu/archive/2011/05/12/asp-net-mvc-3-and-the-helper-syntax-within-razor.aspx).  It will help you get started and understand what Razor is all about.  Start with the previous blog posts he has done from Introducing Razor and go down from there.
- [A Look at the Razor View Engine in ASP.NET MVC](https://www.simple-talk.com/dotnet/asp.net/a-look-at-the-razor-view-engine-in-asp.net-mvc/?utm_source=simpletalk&utm_medium=email-main&utm_content=razorviewengine-20131209&utm_campaign=net) from Dino Esposito is also a good one.
- Working with Razor will introduce you to the [HtmlHelper Class](http://msdn.microsoft.com/en-us/library/system.web.mvc.htmlhelper(v=vs.108).aspx) that will generate the HTML code for you if you so desire.
- For generating HTML table containing your data, the [WebGrid Class](http://msdn.microsoft.com/en-us/library/system.web.helpers.webgrid(v=vs.111).aspx) HTML helper will be useful.  You might need to do your own paging as it does not do server-side paging, meaning every time it goes to a new page it will query the database for all the records, not just the records for that page.
- [Get the Most out of WebGrid in ASP.NET MVC](http://msdn.microsoft.com/en-us/magazine/hh288075.aspx) shows you how to do server-side paging.
- Extension methods will be useful and a good example is [Extending the WebGrid HTML helper](http://stackoverflow.com/questions/11698665/mvc3-web-grid-adding-action-links-at-the-begining-of-columns-list).  To know more about extension methods, see [Extension Methods](http://msdn.microsoft.com/en-us/library/bb383977(v=vs.100).aspx) and [How to: Implement and Call a Custom Extension Method](http://msdn.microsoft.com/en-us/library/bb311042(v=vs.100).aspx).
- [Entity Framework Beginner's Tutoral](http://www.entityframeworktutorial.net/EntityFramework4.3/Introduction.aspx)
- [HTML Tags Reference](http://www.w3schools.com/tags/)
- [HTML DOM Reference](http://www.w3schools.com/jsref/default.asp)
- [CSS Properties Reference](http://www.w3schools.com/cssref/default.asp)
- [learn.jquery.com](http://learn.jquery.com/)
