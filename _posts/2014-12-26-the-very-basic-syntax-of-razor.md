---
title: "The Very Basic Syntax of Razor"
date: "2014-12-26"
categories: 
  - "asp-net-mvc"
---

If you have worked in ASP.NET MVC, you know that the default view engine (or templating engine) is Razor, much like the .aspx/.ascx/.master file templates in ASP.NET Web Forms.  One thing I like about Razor is that you can use C# or VB.NET as the programming language to code in Razor.  All you need to do is learn how to use the Razor syntax.

So here I present to you the very basic syntax you need to know about Razor.  In the code below I am using C#, my preferred language.  You can view the generated HTML page [here](http://rodansotto.com/mvc4/razorcsdemo).

```html
<div\>
    
<h1\>Razor Demo Using C#</h1\>
    
@*  
   Razor comments can be one line or multiple lines.
   Unlike HTML comments, Razor comments are not rendered to the page.
*@
    
@{
   @* You can add Razor comments inside the Razor code block such as this. *@
}
    
@{
   // But why use Razor comments when you can use C# comments.
   /*
    * C# multi-line comment
    */
}
    
@*  
   Razor code starts with @ character.
   It can be a single statement block, an inline expression,
    or a multi-statement block.
   Once you start your code with @, all of the .NET framework,
    ASP.NET, and all the C# features are available to you.
*@
    
@* An example of a Razor single statement block: *@
@{ var myGreeting = "<Hello, World!>"; } 
    
@* 
   Below is an example of a Razor inline expression.
   Note that the output from server code is automatically HTML-encoded.
    < and > characters in the variable myGreeting will automatically
    be encoded to &lt; and &gt; so it can be displayed properly
    in the browser.  You can check the page source to verify this.
*@
<p\>The value of myGreeting is: @myGreeting</p\>
    
@* 
   A Razor inline expression can be multi-token if enclosed in ()
    as in example below.
   Note that () can also be used to explicitly declare a Razor
    inline expression.
*@
<p\>@("The value of myGreeting is: " + myGreeting)</p\>
    
@* Here is an example of a Razor multi-statement block *@
@{
    var myGreeting2 = "Hello, Universe!";
    var myDate = DateTime.Today.ToString("MMMM dd, yyyy");   
}
    
<p\>@myGreeting2 Today is @myDate.</p\>
    
@*
    You will notice in the previous examples of Razor code blocks, 
     be they single or multi-statement blocks, are enclosed in {}.
     They don't have to be always enclosed in {}.
     Take for example the if statement below.  
     Since it is essentially a single statement, 
     it can follow the @ character immediately.
     The same goes with for, foreach, switch, etc.
*@
    
@{ var myMsg = ""; }
    
@if (IsPost) 
{
    myMsg = "This is a postback!";
}
else
{
    myMsg = "This is not a postback.";
}
 
<p\>@myMsg<p\>
    
@*
    You can also mix text and markup in the code block.
*@
    
@if (true)
{
    // Mixing markup in code is as easy as putting in the matching HTML tags.
    <p\>The value of IsPost is: @IsPost</p\>
    
    // You can use @: or <text> to render plain text.
    // If you check the page source, these plain texts are not enclosed in
    //  any HTML tags.
    @:This is plain text.
    <br />
    <text>Another plain text.</text>
    <br />
    <br />
}
    
</div\>
```

Additional Resources:

- [Introduction to ASP.NET Web Programming Using the Razor Syntax (C#)](http://www.asp.net/web-pages/overview/getting-started/introducing-razor-syntax-(c))
- [C# Razor Syntax Quick Reference](http://haacked.com/archive/2011/01/06/razor-syntax-quick-reference.aspx/)
- [ASP.NET Razor from W3Schools](http://www.w3schools.com/aspnet/razor_intro.asp)
