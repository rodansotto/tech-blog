---
title: "HTML, CSS, Javascript, and jQuery: Putting them all together (Part 2)"
date: "2013-05-20"
categories: 
  - "javascript"
  - "web-design"
---

On my previous [post](https://rodansotto.github.io/tech-blog/2013/05/19/web-ui-html-css-javascript-and-jquery-putting-them-all-together-part-1.html), I talked about _HTML_ and _CSS_.  Now I’m going to talk about _Javascript_. 

Javascript is a popular scripting language that makes an HTML page dynamic.  To add Javascript code, you use the _<script>_ tag and you can put them in the _<head>_ or in the _<body>_ section of the HTML page.  It is recommended to put all of them in the _<head>_ section.  Below is an example of a Javascript function being called on a click event of the _<p>_ tag.

<head>  
    <script type="text/javascript"\>  
        function myFunction()   
        {  
            alert("Hello, Universe!!!");  
        }  
    </script>  
</head>  
<body>  
    <p style="font-weight: bold; color: #0000FF" onclick="myFunction()"\>  
        Hello, World!!!  
    </p>  
</body>

  

Remember that Javascript code are executed as the HTML page is being parsed.  The example below will display the message when the HTML page is being loaded without having to wait for any event.  Notice that the Javascript code is not contained in a function declaration like the example above.

<head>  
    <script type="text/javascript"\>  
        alert("Javascript code not belonging to any function");  
    </script>  
</head>

  

If you have lots of Javascript code, it is preferred to put them in an external file with extension _.js_ and use the _<script>_ tag’s _src_ attribute to point to this file.  That way you can also use this file in the other HTML pages.

<head>  
    <script src="MyJavaScript.js"\></script>  
</head>  
<body>  
    <p style="font-weight: bold; color: #0000FF"   
            onclick="myAnotherFunction()"\>  
        Hello, World!!!  
    </p>  
</body>  

  

The file _MyJavascript.js_ contains the following Javascript code:

function myAnotherFunction()  
{  
    alert("Hello, Big Bang!!!");  
}

  

Next post, I’ll cover the _jQuery_.
