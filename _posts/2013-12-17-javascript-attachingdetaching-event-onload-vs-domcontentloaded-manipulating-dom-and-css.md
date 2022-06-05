---
title: "JavaScript: Attaching/Detaching Event, OnLoad vs. DOMContentLoaded, Manipulating DOM and CSS"
date: "2013-12-17"
categories: 
  - "javascript"
---

**Event Handling, Attaching and Detaching Events**

3 phases of event dispatch:

- _Capturing_ – going down the DOM tree until it reaches the target element
- _Target_
- _Bubbling_ – going back up the DOM tree from the target element

// standard way of accessing the Event object  
var eventHandlerDOM = function(evt) {  
    alert(evt.type); //displays click  
}  
      
// starting IE 9 you can use the standard way  
var eventHandlerIE8Older = function() {  
    var evt = window.event;  
    alert(evt.type);  
}  
      
// cross-browser way  
var eventHandlerCB = function(evt) {  
    if (!evt) evt = window.event;  
    alert(evt.type);  
}  
      
window.onload = function() {  
    var btn = document.getElementById("btn");  
      
    // 2 ways of attaching an event  
    btn.onclick = eventHandlerCB;  
    // or ...  
    if (btn.addEventListener) {  
        btn.addEventListener("click", eventHandlerCB, false);  
    }  
    else {  
        // starting IE 9, you can use the standard way using  
        //  addEventListener  
        btn.attachEvent("onclick", eventHandlerCB);  
    }  
      
    alert("events attached");  
    alert("now detaching events...");  
    detachEvents();  
    alert("events detached");      
}  
      
// detaching events  
var detachEvents = function() {  
    if (btn.removeEventListener) {  
        btn.removeEventListener("click", eventHandlerCB, false);  
    }  
    else {  
        // starting IE 9, you can use the standard way using  
        //  removeEventListener  
        btn.detachEvent("onclick", eventHandlerCB);  
    }      
}  

  

**_window.onload_ Event vs. _document.DOMContentLoaded_ event**

The problem with running script on _window.onload_ event is that if you have a rather large image to download, your script will run only after the image is downloaded.  _window.onload_ event is triggered after everything, including external stylesheets, javascript files and images, has been downloaded.  An alternative, and usually a best practice, is to run your script on _document.DOMContentLoaded_ event.

var readyFunc = function() {  
    var stat = document.getElementById("statDOMReady");  
    stat.innerHTML = "DOM is ready!!!";  
}  
      
document.addEventListener("DOMContentLoaded", readyFunc, false);

  

Note that _document.DOMContentLoaded_ event is an _HTML5_ specification.  Also if your script needs to work with CSS, you need to put all your external stylesheets in the header and all your external scripts in the footer so all the styles will be loaded before your scripts are run.

**Manipulating DOM**

A sample of what you can do for manipulating DOM:

- _document.createElement()_ – create an Element node
- _document.createTextNode()_ –  create a Text node
- _element.cloneNode()_ – create a copy of a node and its attributes with option to include the descendants as well
- _element.appendChild()_ – add a new child node as the last child node
- _element.insertBefore()_ – insert a new child node before a specified child node
- _element.removeChild()_ – remove a child node
- _element.replaceChild()_ – replace a child node
- _document.createDocumentFragment()_ – create an imaginary Node object; useful for adding content to your document, or extracting parts of your document and modifying it and inserting it back

**Manipulating CSS**

2 ways to import external stylesheets:

<!-- using <style> tag and @import -->  
<style type\="text/css"\>  
    @import "myStylesheet.css";  
</style\>  
      
<!-- using <link> tag and rel="stylesheet" -->  
<link type\="text/css" href\="myStylesheet.css" rel\="stylesheet" />  
  
  

  

Persistent, preferred, and alternate stylesheets:

<!-- persistent stylesheet -->  
<link type\="text/css" href\="main.css" rel\="stylesheet" />  
      
<!-- preferred stylesheet -->  
<link type\="text/css" href\="dflt.css" rel\="stylesheet" title\="Default" />  
      
<!-- alternate stylesheet -->  
<link type\="text/css" href\="alt1.css" rel\="alternate stylesheet"  
    title\="Alternate 1" />  
  

  

_element.style_, _window.getComputedSyle()_, _element.currentStyle_, elements positioning properties:

var p1 = document.getElementById("p1");  
p1.style.fontSize = "20px";  
      
// standard way of getting the computed style  
var computedStyle = window.getComputedStyle(p1, null);  
alert(computedStyle.fontSize); // displays 20px  
      
// IE way of getting the computed syle  
// starting from IE9, you can use the standard way  
var computedStyle2 = p1.currentStyle;  
alert(computedStyle2.fontSize); // displays 20px  
      
// cross-browser code for getting the computed style  
if ( !("getComputedStyle" in window) ) {  
    alert("getComputedStyle does not exist")  
    window.getComputedStyle = function(element) {  
        return element.currentStyle;  
    }  
}  
      
// positioning properties of an element you can use  
alert(p1.offsetTop);    // displays 130  
alert(p1.offsetLeft);   // displays 8  
alert(p1.offsetHeight); // displays 23  
alert(p1.offsetWidth);  // displays 911  
// below will display 0, because it's parent is the body tag  
alert(p1.offsetParent.offsetTop);  
var body = document.getElementsByTagName("body")\[0\];  
alert(body.offsetTop);  // displays 0
