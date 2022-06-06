---
title: "JavaScript: RegExp, Error, DOM, and Event"
date: "2013-12-09"
categories: 
  - "javascript"
---

This post is a follow-up to my previous posts, [Object Oriented Programming In Javascript](http://rodansotto.wordpress.com/2013/09/21/web-ui-working-with-objects-in-javascript/) and [JavaScript Array and How It’s Different from Object](http://rodansotto.wordpress.com/2013/11/03/web-ui-javascript-array-and-how-its-different-from-object/).  In this post I will touch on regular expressions, error handling, basic DOM scripting, image preloading, and timing events.

**Regular Expressions**

// creating patterns  
var pattern1 = new RegExp("Rodan");     // using constructor  
var pattern2 = /Rodan/;                 // using literal enclosed in "/"  
      
// testing strings against the patterns  
alert(pattern1.test("Rodan Sotto"));    // displays true  
alert(pattern2.test("John Doe"));       // displays false  
      
// using String methods search, match, and replace with regular expressions  
var string1 = "Rodan Sotto";  
var string2 = "John Doe";  
      
// below will display 6, the starting position of the substring found  
alert(string1.search(/Sotto/));   
// below will display -1, which means no substring found  
alert(string2.search(/Sotto/));   
      
alert(string1.match(/Sotto/)); // displays an array \["Sotto"\]  
alert(string2.match(/Sotto/)); // displays null  
      
// below will display "Rodan Nolastname"  
alert(string1.replace(/Sotto/, "Nolastname"));  
// below will display "John Doe"  
alert(string2.replace(/Sotto/, "Nolastname"));  
  

  

See [JavaScript RegExp Object](http://www.w3schools.com/js/js_obj_regexp.asp) for more information.

**Error Handling**

var testErrorHandling = function () {  
    try {  
        alert("Throwing an error inside the try block...");  
        throw(new Error("You've got an error!!!"));  
    }  
    catch (error) {  
        alert(error.message);  
    }  
    finally {  
        alert("Error or not, finally will get executed");  
    }  
};  
  

  

**Basic DOM Scripting**

_W3Schools.com_ has a very good beginner resource on [HTML DOM](http://www.w3schools.com/js/js_htmldom.asp).

- _DOM_ stands for _Document Object Model_.  Everything in DOM is a node.  A Node can be any of the following:
    - Document Node
    - Element Node
    - Attribute Node
    - Text Node
    - Comment Node
- _Document Object_, which represents your web page, is the first object you will need to access the DOM.  It is the root node of the HTML document and the owner of all other nodes.  See [Document Object Properties and Methods](http://www.w3schools.com/jsref/dom_obj_document.asp).
- _Element Object_, which represents an HTML element, is the second object you will need to access the DOM.  Most commonly a call to _document.getElementById()_ method will return an element object.  An element object is also an element node.  It can have child nodes such as _element nodes_, _attribute nodes_, _text nodes_, or _comment nodes_.  See [Element Object Properties and Methods](http://www.w3schools.com/jsref/dom_obj_all.asp).
- An Element Object can be one of the following:
    - [Anchor](http://www.w3schools.com/jsref/dom_obj_anchor.asp) Object
    - [Image](http://www.w3schools.com/jsref/dom_obj_image.asp) Object
    - [Button](http://www.w3schools.com/jsref/dom_obj_button.asp) Object
    - etc., each of which can have it’s own set of properties and method.
- And lastly, the _Attr Object_ which represents an HTML attribute and always belongs to an HTML element.  See [Attr Object Properties and Methods](http://www.w3schools.com/jsref/dom_obj_attributes.asp).
- _Events_.  See [HTML DOM Events](http://www.w3schools.com/jsref/dom_obj_event.asp).  It lists the different events such as:
    - Mouse Events
    - Keyboard Events
    - Frame/Object Events
    - Form Events
    - It also lists the properties and methods of event objects that event handlers have access to such as:
        - Event Object
        - EventTarget Object
        - EventListener Object
        - DocumentEvent Object
        - MouseEvent Object
        - KeyboardEvent Object

**Default Action Cancellation**

var event_handler = function(evt) {  
    if (!evt) evt = window.event;   // for IE  
      
    // ...  
      
    // cancel default action  
    if (evt.preventDefault) {  
        evt.preventDefault();       // for most browsers  
    }  
    else {  
        evt.returnValue = false;    // for IE  
    }  
}  
      
window.onload = function() {  
    var link = document.getElementById("link");  
    link.onclick = event_handler;      
}  

  

**Image Preloading**

var image = new Image();  
image.src = "image.jpg";  
// or  
image.src = link.href;

  

**Timing Events**

JavaScript also provides for executing code at specific time-intervals using _setInterval()_ and _setTimeout()_ methods.  See [JavaScript Timing Events](http://www.w3schools.com/js/js_timing.asp).
