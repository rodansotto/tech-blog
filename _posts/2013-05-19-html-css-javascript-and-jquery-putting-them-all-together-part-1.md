---
title: "HTML, CSS, Javascript, and jQuery: Putting them all together (Part 1)"
date: "2013-05-19"
categories: 
  - "javascript"
  - "web-design"
---

_HTML_ describes how the web page will look like.  Below is an example of an HTML page (created using Visual Studio 2012 by the way).  You have the _<!DOCTYPE>_, _<html>_, _<head>_, and _<body>_ tags as always.

<!DOCTYPE html\>  
<html xmlns\="http://www.w3.org/1999/xhtml"\>  
<head\>  
    <title\>Example HTML Page</title\>  
</head\>  
<body\>  
    <p\> Hello, World!!! </p\>  
</body\>  
</html\>   

  

_CSS_ was created to solve the problem of formatting an HTML page.  Everything that has got to do with style and layout should be done through CSS.  So how do we put CSS in an HTML page?  There are 3 ways:

- _Inline style_.  This is the least preferred way to add CSS because you will be mixing content with presentation.  Below is an example of an inline style.  You have the _style_ attribute added to an HTML tag which can contain any CSS property inside the “”.

<p style\="font-weight: bold; color: #0000FF"\>  
    Hello, World!!!  
</p\>

  

- _Internal style sheet_.  You use this if you want to apply the style throughout the page.  The example below will style all _<p>_ tags that are defined in the HTML page.  You use the _<style>_ tag under the _<head>_ section of the HTML page to contain your CSS declarations.

<head\>  
    <style type\="text/css"\>  
        p {  
            font-family: Arial, Helvetica, sans-serif;  
            font-style: italic;  
            color: #00FF00;  
        }  
    </style\>  
</head\>

  

- _External style sheet_.  This is the preferred method.  Not only is the presentation separate from the content, but it can be reused in other HTML pages.  Below is how you add an external style sheet to an HTML page.  You use the _<link>_ tag under the _<head>_ section of the HTML page.

<head\>  
    <link href\="MyStyleSheet.css" rel\="stylesheet" type\="text/css" />  
</head\>

  

The file _MyStyleSheet.css_ contains the following CSS declarations:

p {border-style: solid; background-color: #00FF00;}

  

_What if we have a CSS property declared in more than one place?_  If that happens, overriding will take place, with the inline style being the highest priority overriding the ones declared in both the internal or external style sheet, with internal style sheet second, and external style sheet third.  Also, if you place the _<link>_ tag after the _<style>_ tag, the external style sheet will override the internal style sheet.

_What is the syntax for declaring CSS property then?_  Easy.  You just have to specify a _selector_ and one or more _declarations_.  Selector would be, in our example above, _p_, an HTML tag.  It can also be the tag's attribute _id_ or _class_, or many others as well which I will be discussing on another post geared towards CSS.

Declarations are the _name: value;_ pairs inside the curly braces _{}_.  In our example above, declarations would be the _{border-style: solid; background-color: #00FF00;}_.  You can see the CSS property _border-style_ is set to _solid_ value.

[W3Schools](http://www.w3schools.com/) has a nice visual way of explaining the CSS syntax:

![](/technical-blog/assets/images/selector.gif)



So that’s it for HTML and CSS.  On my next post, I will be talking about the _Javascript_ and _jQuery_ part.
