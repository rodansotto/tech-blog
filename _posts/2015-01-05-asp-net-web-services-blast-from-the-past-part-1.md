---
title: "ASP.NET Web Services - Blast From The Past (Part 1)"
date: "2015-01-05"
categories: 
  - "asp-net"
---

My last [post](https://rodansotto.github.io/tech-blog/2013/06/11/asp-net-what-are-web-services.html) regarding web services was June 13, 2013 and I ended it with an expectation of a sequel.  Fast forward to today, web services have now been regarded by Microsoft as legacy technologies and recommends using WCF services instead.  Then again, with Web API available why use WCF services if you are only using HTTP for these services?  That will have to be explored on a separate posts.  In this post I will revisit,  hence the title, the basics of creating a web service and the many ways of how to consume it.  I will mostly provide links to avoid reinventing the wheels but still provide my own code and demos as well.

**Creating a Web Service and Consuming It Using WSDL Generated Proxy Class**

[ASP.NET - Web Services from TutorialsPoint](http://www.tutorialspoint.com/asp.net/asp.net_web_services.htm) shows you how to create a web service, how to test the web service locally, and how to consume the web service using proxy.  For this demo, I have created a simple [web service](https://rodansotto.github.io/asmx/translatetofrenchservice.asmx) and a [web page](https://rodansotto.github.io/projects/asmx/UsingProxy.aspx) that consumes it using proxy.

Some important points:

- When creating a new project for a web service in Visual Studio 2010 and up, you need to select _.NET Framework 3.5_ and select the _ASP.NET Web Service Application_ project template.  You can’t create a web service anymore starting version 4.0 of the .NET Framework.
- Make sure to change the _\[WebService(Namespace = ”http://tempuri.org/”)\]_ attribute for your web service class to something unique before you go live with your web service.  I have mine changed below:

```cs
namespace MyWebService { /// <summary> /// Summary description for TranslateToFrenchService /// </summary> \[WebService(Namespace = "https://rodansotto.github.io/")\] \[WebServiceBinding(ConformsTo = WsiProfiles.BasicProfile1_1)\] \[System.ComponentModel.ToolboxItem(false)\] // To allow this Web Service to be called from script, // using ASP.NET AJAX, uncomment the following line. //\[System.Web.Script.Services.ScriptService\] public class TranslateToFrenchService : System.Web.Services.WebService { private string\[,\] translations = { {"good morning", "bonjour"}, {"good evening", "bonsoir"}, {"thank you", "merci"}, {"please", "s'il vous plait"}, {"welcome", "bienvenue"}, {"goodbye", "au revoir"}, {"see you soon", "à bientôt"} };

\[WebMethod\] public string TranslateToFrench(string english) { for (int i = 0; i &lt; translations.GetLength(0); i++) { if (string.Compare( english, translations\[i, 0\], true) == 0) { return translations\[i, 1\]; } } return ""; } } } 
```

- There are also other ways of consuming a web service besides using proxy.  You have HTTP POST method and XMLHTTP.  I will show how to use HTTP POST method later in this post.  As for XMLHTTP, you use the XMLHTTPRequest object in JavaScript.  It’s a lot of work setting this up and the following articles show you how: [Calling a Web Service from Javascript using XMLHttpRequest](http://pavanarya.wordpress.com/2012/05/20/calling-a-web-service-from-javascript-using-xmlhttprequest/) and [Consuming .NET Web Services using XMLHTTP protocol](http://www.codedigest.com/Articles/WebServices/55_Consuming_Webservices_via_XMLHTTP_protocol.aspx).  An alternative way is to use ASP.NET AJAX and [Consuming a Web Service using ASP.NET Ajax](http://www.webreference.com/programming/asp/Ajax_WebService/index.html) shows you how.  But a better way is to use jQuery AJAX which I will also show how later in this post.
- When calling a web service using proxy, you will need to add a web reference.  In Visual Studio 2010 and up, you have the option to add it as a service reference.  In fact Visual Studio is recommending you add it as a service reference rather than a web reference because web reference is using the legacy .NET Framework 2.0 web services technology and is there only for compatibility reason.
    
    - Add as a service reference.  [Walkthrough: Creating and Accessing WCF Services from MSDN](http://msdn.microsoft.com/en-us/library/bb386386.aspx) shows you how to add a service reference.  When you add a service reference, additional config is added to the consuming app’s web.config file under <configuration>.  The following is the config that was added to my web page’s site’s web.config file:
    
    ```xml
    <configuration> <!-- config added for using a service reference --> <system.serviceModel> <bindings> <basicHttpBinding> <binding name="TranslateToFrenchServiceSoap"/> </basicHttpBinding> </bindings> <client> <endpoint address= "https://rodansotto.github.io/asmx/TranslateToFrenchService.asmx" binding="basicHttpBinding" bindingConfiguration="TranslateToFrenchServiceSoap" contract="MyWebServiceB.TranslateToFrenchServiceSoap" name="TranslateToFrenchServiceSoap"/> </client> </system.serviceModel> </configuration> 
    ```
    
    To invoke the web service method using the service reference, I used the following code where _MyWebServiceB_ is the namespace I provided:
    
    ```cs
    protected void Translatev2Button_Click(object sender, EventArgs e) { if (Englishv2TextBox.Text != string.Empty) { try
    
    { // consuming a web service using a service reference MyWebServiceB.TranslateToFrenchServiceSoapClient soapClient = new MyWebServiceB.TranslateToFrenchServiceSoapClient(); Frenchv2Label.Text = soapClient.TranslateToFrench(Englishv2TextBox.Text); }
    
    catch (Exception) { throw; } } } 
    ```
    
    - Add as a web reference.  To add a web reference you have to go to the same _Add Service Reference_ dialog window and click the _Advanced…_ button.  Then click the _Add Web Reference…_ button.  The following are the config added to my web page’s site’s web.config file and also the code I used to invoke the web service method.  You will see the differences between adding as a web reference and adding as a service reference.

```xml
<configuration> <!-- config added for using a web reference --> <applicationsettings> <mywebapp.properties.settings> <setting name="MyWebApp_MyWebService_TranslateToFrenchService" serializeas="String"> <value> https://rodansotto.github.io/asmx/TranslateToFrenchService.asmx </value> </setting> </mywebapp.properties.settings> </applicationsettings> </configuration> 
```

```cs
protected void TranslateButton_Click(object sender, EventArgs e) { if (EnglishTextBox.Text != string.Empty) { try { // consuming a web service using a web reference MyWebService.TranslateToFrenchService service = new MyWebService.TranslateToFrenchService(); FrenchLabel.Text = service.TranslateToFrench(EnglishTextBox.Text); } catch (Exception) { throw; } } } 
```

Ok so that’s how you consume a web service using proxy.  This post has turned out to be longer than I expected so I decided to break this down into multiple parts, thus part 1 of this post ends here.  I will continue with consuming a web service using HTTP POST method on part 2.
