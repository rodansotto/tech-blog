---
title: "CSS Fundamentals"
date: "2013-10-14"
categories: 
  - "web-design"
---

In my last blog [here](http://rodansotto.wordpress.com/2013/05/19/web-ui-html-css-javascript-and-jquery-putting-them-all-together-part-1/), I talked about ways to put CSS in an HTML, the preferred method using external style sheets, and how styles are overwritten when using more than one method.  I also talked about the syntax for declaring a CSS property.

Here I am going to go through some of the basic CSS properties that one would need to know in order to have a good understanding of the capabilities of the CSS, and also a means to brush up one’s CSS knowledge if it ever becomes rusty.  So here they are:

/* comments */  
/*  
 * declaring a CSS property */  
p {  
    border-style: solid;  
}  
/*  
 * declaring multiple CSS properties */  
p {  
    background-color: #00FF00;  
    font-size: 8px;  
}  
/*  
 * setting font-size using em which is a relative measure  
 * 1em = default font size, 2em = twice as big, and 0.5em = half the size */  
p {  
    font-size: 2em;  
}  
/*  
 * declaring fall back fonts in case user's computer does not have the font  
 * note CSS has default fonts and they are serif, sans-serif, and cursive */  
p {  
    font-family: Verdana, serif;  
}  
/*  
 * styling a table's border property to 1px, solid line, and color black */  
table {  
    border: 1px solid black;  
}  
/*  
 * styling a link's text-decoration property to hide the underline */  
a {  
    text-decoration: none;  
    color: #cc0000;  
}  
/*  
 * creating a button  
 * use border-radius property to give the button a rounder look  
 * use margin: auto to put equal left and right margin on the button,  
 *  centering it on the page  
 * use text-align to set alignment of text inside the button */  
div {  
    height: 50px;  
    width: 120px;  
    border: 2px solid #6495ed;  
    background-color: #bcd2ee;  
    border\-radius: 5px;  
    margin: auto;  
    text-align: center;  
}  
/*  
 * styling every element on the page using the universal (*) selector */  
* {  
    color: black;  
}  
/*  
 * styling an element nested somewhere inside another element or  
 *  is a child of another element using nested selectors */  
div h3 {  
    color: red;  
}  
/*  
 * styling an element nested directly inside another element or  
 *  is a direct child of another element */  
body \> div \> p {  
    color: #7ac5cd;  
}  
/*  
 * note that more specific selectors will override other selectors  
 * e.g. <p> selector will be overridden by nested selector body > div > p  
 * nested selectors can be overridden too by the class and id selectors */  
/*  
 * so far we have used HTML element selectors and the universal selector */  
/*  
 * styling using the class selector - the . selector */  
.myClass {  
    font-family: cursive;  
    color: #0000cd;  
}  
/*  
 * styling using the id selector - the # selector */  
#myID {  
    font-family: Courier;  
    color: #cc0000;  
}  
/*  
 * note that the id selector is more specific than the class selector,  
 * thus the id selector will override the class selector */  
/*  
 * using pseudo-class selectors - the : selector,  
 *  to select HTML items not part of the document tree */  
/*  
 * styling a link's unvisited link */  
a:link {  
    text-decoration: none;  
    color: #008b45;  
}  
/*  
 * styling a link's visited link */  
a:visited {  
    color: #ee9a00;  
}  
/*  
 * styling a link when it's hovered over by the mouse */  
a:hover {  
    color: #00ff00;  
}  
/*  
 * styling elements that are the first children of their parents */  
p:first-child {  
    font-family: cursive;  
}  
/*  
 * styling elements that are not the first children of their parents - 
 *  the second, or the third, and so on... */  
p:nth-child(2) {  
    font-family: Tahoma;  
}  
/*  
 * CSS positioning */  
/*  
 * positioning using the display property  
 * 4 possible values:  
 * block - stacks the elements on top of each other like blocks in a column  
 * inline-block - puts the elements next to each other like blocks in a row  
 * inline - puts the elements next to each other but not as blocks:  
 *  they don't keep their dimensions  
 * none - hides the element and it's contents from the page */  
div {  
    height: 50px;  
    width: 100px;  
    border: 2px solid black;  
    border\-radius: 5px;  
    display: block;  
}  
/*  
 * CSS box model  
 * every element follows the box model in CSS,  
 *  where each element contains the content surrounded by padding, which  
 *  in turn is surrounded by border, which in turn is surrounded by margin  
 * margin is the space around the element,  
 *  the space between the element and the elements around it  
 * border is the edge of the element; set using the border property  
 * padding is the space between the border and the content of the element  
 * content is the actual stuff  
/*  
 * setting the margin using margin: auto */  
div {  
    height: 50px;  
    width: 120px;  
    border: 2px solid #6495ed;  
    background-color: #bcd2ee;  
    margin: auto;  
}  
/* setting the margin using margin: top right bottom left */  
div {  
    height: 50px;  
    width: 120px;  
    border: 2px solid #6495ed;  
    background-color: #bcd2ee;  
    margin: 20px 50px 10px 5px;  
}  
/* setting the margin using margin-top, margin-right, margin-bottom,  
 *  and margin-left properties */  
div {  
    height: 50px;  
    width: 120px;  
    border: 2px solid #6495ed;  
    background-color: #bcd2ee;  
    margin\-top: 20px;  
    margin\-right: 50px;  
    margin\-bottom: 10px;  
    margin\-left: 5px;  
}  
/*  
 * note that you can use negative values on the margins,  
 *  which will move the element in the other direction */  
/*  
 * setting the padding is similar to setting the margin  
 * you can use padding property to set top, right, bottom, left padding  
 * you can use padding property to give it one value,  
 *  to apply same value of padding on all sides  
 * or you can use the padding-top, padding-right, padding-bottom,  
 *  and padding-left properties */  
div {  
    height: 50px;  
    width: 120px;  
    border: 2px solid #6495ed;  
    background-color: #bcd2ee;  
    padding: 10px;  
}  
/*  
 * positioning using the float property  
 * setting float to right will put the element on right side of the page  
 * setting float to left will put the element on left side of the page */  
div {  
    height: 50px;  
    width: 120px;  
    border: 2px solid #6495ed;  
    background-color: #bcd2ee;  
    float: right;  
}  
/*  
 * note that floating elements will go on top of non-floating elements,  
 *  unless you set the clear property to the following values:  
 * left will move the non-floating element below any floating elements  
 *  on the left side  
 * right will move the non-floating element below any floating elements  
 *  on the right side  
 * both will move it below any floating elements on left and right sides */  
div {  
    height: 50px;  
    background-color: #69D2E7;  
    clear: both;  
}  
/*  
 * positioning using the position property  
 * CSS positioning, by default, is static,  
 *  meaning elements are positioned where they would normally go  
 * setting position to absolute will position the element relative  
 *  to the first parent element that does not have a static position  
 * if there is no such element then it is positioned relative to <html>  
 * setting position to relative will position the element relative  
 *  to where it would have been placed if it had a default static position  
 * setting position to fixed will anchor the element to the browser window  
 *  and stays put even when you scroll up or down */  
div {  
    height: 50px;  
    background-color: #69D2E7;  
    position: fixed;  
}  
  

  

You could also look at this [link](http://www.codecademy.com/glossary/css) for a quick review of CSS basics.
