---
title: "ASP.NET 2.0: Crystal Reports – Fitting the report inside the available space in your web page"
date: "2009-04-01"
categories: 
  - "asp-net"
---

If you prefer displaying a crystal report to a web page where you have other stuff in it (like say a top and left menu bar with a bottom footnote), and you want to display it on the available space in the web page (not on the whole web page), and you find it spilling over, don’t worry there is a solution to that.

When you drop the **CrystalReportsViewer** control on your web page design surface, there is a property in it that gets set to **True** by default and its the main reason why its spilling over to the rest of your web page.  This property is the **BestFitPage**.  By setting this property to **False** and at the same time setting the **Height** and **Width** properties, the report will be displayed within the boundary you set and scrollbars will be provided automatically for you if necessary to view the whole report.
