---
title: "ASP.NET MVC 5: OWIN/Katana Pipeline And Middleware Components (A Demo)"
date: "2017-11-01"
categories: 
  - "asp-net-mvc"
---

![](/technical-blog/assets/images/myprojects.png)

[DEMO](http://www.rodansotto.com/mvc5/HelloWorldOWINPipeline) | [CODE](http://www.rodansotto.com/projectcode/helloworldowinpipeline01.aspx) | [MY (Other) PROJECTS](http://www.rodansotto.com/myprojects.aspx)



If you know [ASP.NET Core](https://mva.microsoft.com/en-us/training-courses/introduction-to-asp-net-core-with-visual-studio-2017-16841?l=JWZaodE6C_5706218965), you will notice some similarities between that and [Katana](https://docs.microsoft.com/en-us/aspnet/aspnet/overview/owin-and-katana/an-overview-of-project-katana).  That is because both of them supports [OWIN:](http://owin.org/) Katana bringing OWIN support to ASP.NET; and ASP.NET Core natively supporting OWIN.

In this demo, using ASP.NET MVC 5, I registered my OWIN middleware components in the _Configuration(IAppBuilder)_ method of the _Startup_ class declared in _Startup.cs_ by calling one of the these methods: _IAppBuilder.Use()_, or an _IAppBuilder_ extension method that wraps _IAppBuilder.Use()_,  or _IAppBuilder.Run()_.  This [code](http://www.rodansotto.com/projectcode/helloworldowinpipeline01.aspx) explains it a little bit more.

I declared all my OWIN components in a separate file named _Startup.MyOWINComponents.cs_.  Each component adds a _Hello World!!!_ string in their own language to an OWIN environment variable and awaits the next component in the pipeline, and once the last component is done it passes control back to the previous component until the first component in the pipeline outputs the resulting string to response.  This [code](http://www.rodansotto.com/projectcode/helloworldowinpipeline02.aspx) explains it a little bit more.

The [demo](http://www.rodansotto.com/mvc5/HelloWorldOWINPipeline) displays the following:

## Hello World!!! Bonjour Tout Le Monde!!! Mabuhay!!!
