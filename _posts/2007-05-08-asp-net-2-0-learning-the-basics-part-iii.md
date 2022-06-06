---
title: "ASP.NET 2.0: Learning the Basics, Part III"
date: "2007-05-08"
categories: 
  - "asp-net"
---

**Page Load Event**

**Page Load** event is fired when the page is loaded and accessed for the first time and when it is loaded in response to a client postback.  But if you need to initialize variables or want something to happen only once during the first load of the page, you can use the **IsPostBack** property of the **Page** object to determine if the page is loaded for the first time or due to postback:

    Protected Sub Page_Load(ByVal sender As Object, ByVal e As System.EventArgs) Handles Me.Load
        If Not Page.IsPostBack Then
            ' do some initialization here...
        End If
    End Sub

**Application and Session Events**

If you need to code on the application and/or session events, add the **Global.asax** file (**Add New Item...** and select **Global Application Class)**.  You will find 3 application events (**Start**, **End**, and **Error**) and 2 session events (**Start** and **End**).

**Application and Session State**

As always, you can save your application and session states using the Application and Session objects respectively:

Application("MyAppVariable") = "MyAppValue"

and

Session("MySessionVariable") = "MySessionValue"

**Session Identifiers**

To identify each browser session, ASP.NET assigns a unique ID to a session, the **SessionID** property of the **Session** object.

**ViewState Object**

ViewState object is useful in persisting data on the page between postbacks.  It makes use of the **__VIEWSTATE** input hidden field that is inserted into the generated page.  __VIEWSTATE contains the state of all the controls on the page in encrypted form.

**Profile Object**

New in ASP.NET 2.0 is the **Profile** object.  This is now the preferred way to store user information across multiple visits to a web application.  It's like the Session object but better.  It is strongly typed and you have the option to save it in the database, in an XML file, or in memory. 

To add properties to your Profile object, you need to add them to your web.config file, inside the **<system.web>** element:

<configuration\>
   <appSettings/>
   <connectionStrings/>
   <system.web\>

      ...

      <anonymousIdentification enabled\="true" />
      <profile\>
         <properties\>
            <add name\="MyProfileVariable" allowAnonymous\="true" />
         </properties\>
      </profile\>
    
  </system.web\>
</configuration\>

In your code you can access or set the property like this:

    Profile.MyProfileVariable = "MyValue"

**Other ASP.NET Objects**

Other objects that are also available in ASP.NET are the following: **Request**, **Form**, **Trace**, **User**, **Server**, and **PreviousPage**.

**Query String**

To pass data from one page to another, you can use the name/value pair in the query string of the URL:

MyW[ebPage.aspx?MyVariable=MyValue](http://www.mywebsite.com/mywebpage.aspx?MyVariable=MyValue)

On the target page, you can access the value in the query string using the **Request** object:

Request.QueryString("MyVariable")

**Cross Page PostBack**

New in ASP.NET 2.0 is the ability to postback to a different page.  To use this, set the **PostBackUrl** property of the **Button** control to the page that you want to postback to.  To get information from the source page, you can use the **PreviousPage** object or the **Form** dictionary of the **Request** object.  If you want to check if the target page is running as a result of a cross page postback, use the **IsCrossPagePostBack** property of the **PreviousPage** object.  Do not use the target page's **IsPostBack** property as it is set to false.
