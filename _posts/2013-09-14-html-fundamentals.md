---
title: "HTML Fundamentals"
date: "2013-09-14"
categories: 
  - "web-design"
---

Below are the fundamentals that you need to know to start creating HTML pages.  Good for brushing up your HTML skills if you feel you forgot them already.

<!-- comments -->  
<!-- tags are those enclosed in <> like <html> and <head> -->  
<!-- most tags have opening and closing tags like <p> and </p> -->  
<!-- few tags are self-enclosing tags like <img /> -->  
<!-- from opening tag to closing tag is what is called an element -->   
<!-- attributes are name="value" pairs like in <p id="p1"> -->  
<!DOCTYPE html\>  
<html\></html\>  
    <head\></head\>  
        <title\></title\>  
        <link type\="text/css" rel\="stylesheet" href\="stylesheet.css" />  
    <body\></body\>  
        <p\></p\>  
        <strong\></strong\> <!-- to bold text -->  
        <em\></em\> <!-- to italicize text -->  
        <h1\></h1\> to <h6\></h6\>  
        <img src\="image.jpg" />  
      
        <a href\="URL"\>this is a text link</a\> <!-- text link -->  
        <a href\="URL"\><img src\="image.jpg" /></a\> <!-- image link -->  
      
        <ul\> <!-- you can nest lists -->  
            <li\></li\>  
        </ul\>  
        <ol\>  
            <li\></li\>  
        </ol\>  
      
        <!-- attributes for styling text (inline style) -->  
        <p style\="color:blue; font-size:10px; font-family:Courier"\>  
        <body style\="background-color:brown"\>  
        <h3 style\="text-align:center"\>  
      
        <table\>  
            <thead\>  
                <tr\> <!-- row header -->  
                    <th\></th\> <!-- column header -->  
                </tr\>  
            </thead\>  
            <tbody\>  
                <tr\>  
                    <td\></td\>  
                </tr\>  
            <tbody\>  
        </table\>  
      
        <!-- attributes for styling table (inline style) -->  
        <td colspan\="2″ style="border:1px solid black"\>  
          
        <div\></div\> <!-- for dividing webpage into smaller pieces --->  
          
        <!-- attributes for styling div (inline style) -->  
        <div style\="width:50px; height:50px"\></div\>  
          
        <span\></span\> <!-- for styling even smaller parts like text -->  
        <p\>This is black, this is <span style\="color:red"\>red</span\>!</p\>  
      
        <!-- NOTE:  
            <div> is a block level element  
            <span> is an inline level element  
            Block level element has new lines before and after  
             and consumes the whole width available  
            Inline level element has no new lines,  
             can be placed aside other elements  
             and cannot define width  
        -->  
  

  

You could also look into this [link](http://www.codecademy.com/glossary/html) for a quick review of HTML basics.
