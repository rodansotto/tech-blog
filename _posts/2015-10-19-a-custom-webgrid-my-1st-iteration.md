---
title: "A Custom WebGrid (My 1st Iteration)"
date: "2015-10-19"
categories: 
  - "asp-net-mvc"
---

[DEMO](http://rodansotto.com/mvc4/WebGridDemo1) | [CODE](http://rodansotto.com/projectcode/webgriddemo1controller.aspx)

To display tabular data in ASP.NET MVC (I’m using MVC 4 at the time), I used the web helper [WebGrid](https://msdn.microsoft.com/en-us/library/system.web.helpers.webgrid(v=vs.111).aspx).  It has sorting and paging but no filtering.  Also sorting and paging is only client-side and not server-side, meaning all the data is requested from the server and sorted and paged on the client.  Because of these limitations I had to customize WebGrid and this [demo](http://rodansotto.com/mvc4/WebGridDemo1) is my first iteration.

Here in this demo I used Entity Framework to get my data access layer going.  I used the Adventure Works 2008R2 SQL database, the light version.  Here I am displaying the Products table.  To get my UI going, I used the default template that comes with Visual Studio 2010 and it uses jQuery UI.  My second iteration of this custom WebGrid will be using Bootstrap and is still in the works, just FYI.

If you find that you cannot reference WebGrid in your view, there is a chance that System.Web.Helpers is not added to your References.  Add that and set Copy Local to True.  Search Google if you are having problems with this.

You can copy and paste the [code](http://rodansotto.com/projectcode/webgriddemo1controller.aspx) into your own project but you have to change the column names in the WebGrid, add these same columns to sort on in the controller, and change the fields you want to filter on in both view and controller.  Also, you can change the default page size in the FilterSortPageInfo class.  Oh by the way, this is a read-only WebGrid and there is no edit or add functionality.  Cheers!

![]({{ site.baseurl }}/assets/images/myprojects.png)


