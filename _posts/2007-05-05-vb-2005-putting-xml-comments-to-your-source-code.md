---
title: "VB 2005: Putting XML comments to your source code"
date: "2007-05-05"
categories: 
  - "vb-net"
---

A new feature in Visual Studio 2005 is the ability to add XML comments to your procedures and functions and even classes, which can be picked up by Visual Studio's **IntelliSense** besides providing means to generate documentation and help files for the source code. 

To add the XML comments, type 3 single quotes (**'''**) to the line before the procedure or function and Visual Studio will add the following block of comments:

    ''' <summary>
    ''' 
    ''' </summary>
    ''' <param name="sender"></param>
    ''' <param name="e"></param>
    ''' <remarks></remarks>

What you have now is a template where you can enter your description and parameters for the procedure or function you want to document or comment on.

You will find an XML file containing all the XML comments in your project directory when you compiled your project.  You can use this to generate the documentation and help files.
