---
title: "ASP.NET Web Services - Blast From The Past (Part 2)"
date: "2015-01-06"
categories: 
  - "asp-net"
---

Here is part 2 of this topic as promised.  It will cover consuming web service using HTTP POST and using jQuery AJAX.  If you missed part 1 of this topic, click [here](https://rodansotto.github.io/tech-blog/2015/01/05/asp-net-web-services-blast-from-the-past-part-1.html).

But before I start, I forgot to mention in part 1 that when you set up your web service as part of a web site, like when you deploy your web service in a virtual directory of a web site, you need to make sure the _<compilation>_ setting in the web site’s _web.config_ file does not have the _targetFramework_ attribute which is usually present when targeting .NET Framework 4.0 and up.  Otherwise, your web service will not work.  Ok, so on to part 2.

**Consuming a Web Service Using HTTP POST**

Another article that covers the basics of a web service including consuming it using HTTP POST is [Understanding the Basics of Web Service in ASP.NET](http://www.codeproject.com/Articles/337535/Understanding-the-Basics-of-Web-Service-in-ASP-NET).  I have a demo [web page](https://rodansotto.github.io/projects/asmx/UsingHTTPPost.aspx) that uses HTTP POST to consume the simple [web service](https://rodansotto.github.io/asmx/translatetofrenchservice.asmx) I created.

Some important points:

- When you use this method, you need to add the below config to the web service’s _web.config_ file, otherwise you will get this [error](http://stackoverflow.com/questions/657313/request-format-is-unrecognized-for-url-unexpectedly-ending-in).

```xml
<configuration> <system.web> <!-- enable HttpGet and HttpPost on the web service --> <webservices> <protocols> <add name="HttpGet" /> <add name="HttpPost" /> </protocols> </webservices> </system.web> </configuration> 
```

- The response you get will be displayed in the browser in XML format (see my demo [web page](https://rodansotto.github.io/projects/asmx/UsingHTTPPost.aspx)).  If you want to handle the response, you need to code to send a POST request and handle the response, as in below:

```cs
protected void Translatev2Button_Click(object sender, EventArgs e) { if (EnglishTextBox.Text != string.Empty) { try { // this is the content of the request byte\[\] content = System.Text.Encoding.ASCII.GetBytes( "english=" + EnglishTextBox.Text);

// create the request System.Net.WebRequest request = System.Net.HttpWebRequest.Create( "https://rodansotto.github.io/asmx/" + "TranslateToFrenchService.asmx/TranslateToFrench"); request.Method = "POST"; request.ContentType = "application/x-www-form-urlencoded"; request.ContentLength = content.Length;

// write the content to the request stream System.IO.Stream requestStream = request.GetRequestStream(); requestStream.Write(content, 0, content.Length); requestStream.Flush();

// get the response System.Net.WebResponse response = request.GetResponse(); // get the stream associated with the response System.IO.Stream responseStream = response.GetResponseStream(); // pipes the stream to a higher level stream reader with the // required encoding format System.IO.StreamReader streamReader = new System.IO.StreamReader( responseStream, System.Text.Encoding.UTF8);

// the response is in XML format and normally needs to be handled // but since the XML response is simple enough that when displayed // by the browser, it only displays what we need to display, // the french text FrenchLabel.Text = streamReader.ReadToEnd(); } catch (Exception) { throw; } } } 
```

**Consuming a Web Service Using jQuery AJAX**

Another way to call a web service is by using [jQuery.ajax()](http://api.jquery.com/jquery.ajax/) function.  This is the preferred way by many.  [Understand jQuery Ajax Function: Call Web Service Using jQuery Ajax Method](http://www.c-sharpcorner.com/UploadFile/dacca2/understand-jquery-ajax-function-call-web-service-using-jque/) shows you how.  Below is the client-side code for my demo [web page](https://rodansotto.github.io/projects/asmx/UsingJQueryAJAX.aspx) that uses jQuery AJAX to consume the simple [web service](https://rodansotto.github.io/asmx/translatetofrenchservice.asmx) I created.

```js
<head runat="server"> <script src="http://ajax.googleapis.com/.../1.11.2/jquery.min.js"> </script> <script> $(document).ready(function () { $("#TranslateButton").click(function () { // have to add following statement to enable cross-domain request $.support.cors = true;

$.ajax({ type: "POST",

url: "https://rodansotto.github.io/...Service.asmx/TranslateToFrench",

//contentType: "application/x-www-form-urlencoded; charset=UTF-8", // no need to specify contentType above as that is the default

data: "english=" + $("#EnglishTextBox").val(),

dataType: "text",

success: function (response) { $("#FrenchLabel").html(response); },

error: function (jqXHR, textStatus, errorThrown) { var errorMsg = "jQuery AJAX ERROR!!!\\njqXHR.statusText = " + jqXHR.statusText + "\\ntextStatus = " + textStatus + "\\nerrorThrown = " + errorThrown; alert(errorMsg); } }); }); }); </script>

```

Some important points:

- If your web app will be making a cross-domain request to call the web service, you need to set _$.support.cors = true_, otherwise you will receive the [‘No Transport’](http://stackoverflow.com/questions/9160123/no-transport-error-w-jquery-ajax-call-in-ie) error.
- And don’t forget to enable the following attribute in your web service class: _\[System.Web.Script.Services.ScriptService\]_.

```cs
namespace MyWebService { /// <summary> /// Summary description for TranslateToFrenchService /// </summary> \[WebService(Namespace = "https://rodansotto.github.io/")\] \[WebServiceBinding(ConformsTo = WsiProfiles.BasicProfile1_1)\] \[System.ComponentModel.ToolboxItem(false)\] // To allow this Web Service to be called from script, // using ASP.NET AJAX, uncomment the following line. \[System.Web.Script.Services.ScriptService\] public class TranslateToFrenchService : System.Web.Services.WebService { 
```

And that concludes this topic ASP.NET Web Services - Blast From The Past.
