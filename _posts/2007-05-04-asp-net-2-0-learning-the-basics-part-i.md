---
title: "ASP.NET 2.0: Learning the Basics, Part I"
date: "2007-05-04"
categories: 
  - "asp-net"
---

I will probably be very brief about this and just go through the important ones, the ones that you need to know if you're coming from classic ASP just like me.

**Creating a Webpage**

When you create your ASP.NET web site (**File -> New Website...** and select **ASP.NET Web Site** from the templates), **Default.aspx** file is created and probably the **web.config** file too.  When you start coding your events on the controls you placed on your Default web page, a code-behind file named **Default.aspx.vb** is created.  This is because by default, code is separated from the HTML.  You still have the option though to have your code inside the HTML by removing the check on the **Place code in separate file** checkbox when you create a new web page (**Add New Item...** and select **Web Form** from the templates).

**Laying Out Controls**

Besides using **Tables** to layout your controls you can use **Absolute Positioning**.  To set absolute positioning to all your controls, go to **Layout -> Position -> Auto-position Options...** and check the **Change positioning to the following for controls added using the Toolbox, paste, or drag and drop:** checkbox and make sure **Absolutely positioned** is selected in the drop down list.  Once set you can move your controls anywhere you like.  You can also set the absolute positioning of each control by selecting the control and going to **Layout -> Position** and selecting **Absolute**.

Another way to layout your controls is to use **Layers** (**Layout -> Insert Layer**).  These are absolute positioned areas where you can place your controls and then basically move the layer to where you want it to be.

**Standard Controls**

The following are just some of the ASP.NET server controls that you can place on to your web page: **Labels**, **TextBox**, **DropDownList**, **RadioButton**, **CheckBox**, **HyperLink**, and **Buttons**.  One thing to remember about using radio button controls, when you only want one of them selected, is to set their **GroupName** properties to some name.  For the hyperlink controls, you set the **NavigationUrl** property to some URL that you would like to navigate to when this hyperlink is clicked.
