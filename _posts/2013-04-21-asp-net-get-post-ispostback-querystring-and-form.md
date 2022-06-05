---
title: "ASP.NET: GET, POST, IsPostBack, QueryString, and Form"
date: "2013-04-21"
categories: 
  - "asp-net"
---

I have been asked a couple of times in my job interviews about **GET**, **POST**, **IsPostBack**, **QueryString**, and **Forms**.  These are the basics that one who has worked on ASP.NET should know.  Sometimes you get focused on higher level stuff especially if you are working with wrappers or some sort of framework on top of ASP.NET that you lose focus on the basics.  It happens.  At least to me it happens.

So what is **GET**?  **GET** is one of the most common HTTP commands, just like POST, that is sent by the browser to the web server.  It tells the web server to get or fetch a page for the browser.  So when you type a URL

[http://rodansotto.wordpress.com](http://rodansotto.wordpress.com)

 

on your browser's address window and press ENTER, the browser sends a GET command to the web server and the web server fetches the page and sends it back to the browser and the browser displays the page.  Simple.

**POST**, on the other hand, is sent by the browser to the web server if it needs to post or send back data or information to the web server.  So when you fill up information on a web page, say maybe you are creating a new user account, and pressed a submit button, the browser sends a POST command, attaches the information you entered and sends it to the web server.

**IsPostBack** is a property of the **Page** class representing a **Web Forms** page in **ASP.NET**.  You use this property to check if the page is being loaded or rendered or being requested for the first time (a GET command) as opposed to being loaded as a response to a postback (a POST command).

Querystring is the string you see in a URL after the **?** character

[http://search.microsoft.com/en-ca/results.aspx?form=MSHOME&setlang=en-ca&q=asp.net](http://search.microsoft.com/en-ca/results.aspx?form=MSHOME&setlang=en-ca&q=asp.net)

 

It allows you to pass data from one page to another.  It can contain more than one name/value pair

form=MSHOME
setlang=en
q=asp.net

 

separated by the **&** character.  On the target page (e.g. **results.aspx**) one can access the name/value pair using the **QueryString** collection of the **Request** object

Request.QueryString("form");
Request.QueryString("setlang");
Request.QueryString("q");

 

**Form** collection is another property of the **Request** object that allows you to access the information sent by the browser through a POST command.  It retrieves the values of the form elements.  So if we have the following form tag:

<form method\="POST" action = "getCustomer.aspx" \>
    Enter Customer ID:
    <input type\="text" name\="Id"\>
    <input type\="submit" value\="Get Customer"\>
</form\>

 

we can retrieve the customer ID using the following code:

Request.Form("Id");
