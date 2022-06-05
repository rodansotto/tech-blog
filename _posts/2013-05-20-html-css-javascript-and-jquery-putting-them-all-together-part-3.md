---
title: "HTML, CSS, Javascript, and jQuery: Putting them all together (Part 3)"
date: "2013-05-20"
categories: 
  - "javascript"
  - "web-design"
---

_jQuery_ is one of the Javascript frameworks out there, and it’s the most popular.  Basically it lets you write less Javascript code and do complicated things using simple calls to the framework. 

To use jQuery in your HTML page, first you need to download the library from it’s website [jQuery.com](http://jquery.com/).  Just like adding an external Javascript file, you can point to the jQuery library you just downloaded using the _<script>_ tag’s _src_ attribute. 

Another way to add jQuery to your HTML page without downloading and hosting it yourself, is to include it from a _CDN (Content Delivery Network)_  like Google and Microsoft.  You can save download time this way if users have visited others sites that point their jQuery to one of these CDNs.

jQuery’s syntax revolves around the idea of selecting or querying HTML elements and performing action on the elements.  Below is the basic syntax:

$(selector).action() 

  

The $ indicates it’s a jQuery.  So if you see $ in an HTML page source, you know it’s using jQuery.  The selector is pretty much like the CSS selector.  The action defines what action needs to be done on the selected element.  Below is an example jQuery code:

<head>  
    <script src="//ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.min.js"\>  
        </script>  
    <script>  
        $(document).ready(function(){  
            $("p").click(function(){  
                alert("I'm a jQuery code!!!");  
            });  
        });  
    </script>  
</head>   

  

In the example above, I pointed my jQuery library to Microsoft’s CDN in the first _<script>_ tag.  My jQuery code is located on the second _<script>_ tag.  What it does is display a message when the _<p>_ tag is clicked, same as in my previous post but this time using jQuery.  It still uses Javascript coding but it adds it’s jQuery syntax on top of it.  You will notice that the code is wrapped inside the jQuery document ready event.  This is the usual practice when doing jQuery to ensure that the document is fully loaded.

So now you know how _HTML_, _CSS_, _Javascript_, and _jQuery_ ties together, it’s time to move forward to more meaty stuff, get more familiar and learn more about what these technologies can do.  This ends my 3-part post on this topic.  Below are the links to my other parts of this post:

- [Web UI: HTML, CSS, Javascript, and jQuery: Putting them all together (Part 1)](http://rodansotto.wordpress.com/2013/05/19/web-ui-html-css-javascript-and-jquery-putting-them-all-together-part-1/)
- [Web UI- HTML, CSS, Javascript, and jQuery- Putting them all together (Part 2)](http://rodansotto.wordpress.com/2013/05/20/web-ui-html-css-javascript-and-jquery-putting-them-all-together-part-2/ "Web UI- HTML, CSS, Javascript, and jQuery- Putting them all together (Part 1)")
