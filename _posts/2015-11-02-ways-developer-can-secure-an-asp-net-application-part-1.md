---
title: "Ways Developer Can Secure An ASP.NET Application, Part 1"
date: "2015-11-02"
categories: 
  - "asp-net"
---

![]({{ site.baseurl }}/assets/images/secureaspnetlogo.png)

- Don’t turn off request validation unless you need to.  [Request Validation in ASP.NET](https://msdn.microsoft.com/en-us/library/hh882339(v=vs.110).aspx) explains what this feature does, how to disable it if you must in Web Forms, MVC, and Web Pages and how to manually validate request in absence of it.
- To mitigate [Cross-Site Scripting (XSS)](https://www.owasp.org/index.php/Cross-site_Scripting_(XSS)) attack, encode any input that you output via [Response.Write()](https://msdn.microsoft.com/en-us/library/1463ysyw(v=vs.110).aspx), [embedded code block <%= %>](https://msdn.microsoft.com/en-us/library/ms178135(v=vs.100).aspx) or by setting a property on a control that produces text within a page,  using [HttpUtility.HtmlEncode()](https://msdn.microsoft.com/en-us/library/73z22y6h(v=vs.110).aspx)  or [HttpUtility.UrlEncode()](https://msdn.microsoft.com/en-us/library/4fkewx0t(v=vs.110).aspx).  [HttpUtility Methods](https://msdn.microsoft.com/en-us/library/system.web.httputility_methods(v=vs.110).aspx) contains all the encoding and decoding methods for html, html attribute, javascript, query string, and url.
- There is a new embedded code block syntax in ASP.NET 4 that automatically HTML encode output, the [<%: %>](http://weblogs.asp.net/scottgu/new-lt-gt-syntax-for-html-encoding-output-in-asp-net-4-and-asp-net-mvc-2).
- Use [Microsoft AntiXSS Library](https://wpl.codeplex.com/) which extends the built-in encoding methods, provides extra output types like XML, and uses a white-listing approach that defines a list of valid characters (as opposed to the standard .NET framework encoding’s black-listing approach that defines a list of invalid characters).  If using .NET 4.x, a version of AntiXSS is already included under [System.Web.Security.AntiXss Namespace](https://msdn.microsoft.com/en-us/library/system.web.security.antixss(v=vs.110).aspx).  You can have the .NET framework use the AntiXSS library by default by registering it via web.config in [system.web/httpRuntime, attribute encoderType](https://msdn.microsoft.com/en-us/library/e1f13641(v=vs.100).aspx).  See remarks in [AntiXssEncoder](https://msdn.microsoft.com/en-us/library/system.web.security.antixss.antixssencoder(v=vs.110).aspx) on how to do this.
- Beginning in .NET 5, a white list based encoder will be the only encoder.
- If you must output certain black listed HTML elements in the input, good practice is to first encode the whole input and then selectively decode those that you wish to output as is.
- Use [HttpOnly](https://www.owasp.org/index.php/HttpOnly#Using_.NET_to_Set_HttpOnly) to protect cookies from being read by client-side scripts, thus prevents being stolen by an XSS attack.  You can set it via web.config in [system.web/httpCookies element](https://msdn.microsoft.com/en-us/library/vstudio/ms228262(v=vs.100).aspx) or programmatically using [HttpCookie.HttpOnly](https://msdn.microsoft.com/en-us/library/system.web.httpcookie.httponly(v=vs.110).aspx).
- See [OWASP Top 10 for .NET developers part 2: Cross-Site Scripting (XSS)](http://www.troyhunt.com/2010/05/owasp-top-10-for-net-developers-part-2.html).
- Avoid using direct object references such as filenames and database record IDs in your query string, a vulnerability called [Insecure Direct Object Reference](https://www.owasp.org/index.php/Top_10_2013-A4-Insecure_Direct_Object_References).  Use another key, index, map or indirect method such as GUID for example.  If it must be used, make sure user is authorized first.
- See [OWASP Top 10 for .NET developers part 4: Insecure direct object reference](http://www.troyhunt.com/2010/09/owasp-top-10-for-net-developers-part-4.html).
- Never put sensitive information on hidden form fields.
- Never use the [Request indexer](https://msdn.microsoft.com/en-us/library/system.web.httprequest.item(v=vs.110).aspx) to access input by name.  Be specific when looking for input by using [Request.QueryString](https://msdn.microsoft.com/en-us/library/system.web.httprequest.querystring(v=vs.110).aspx), [Request.Form](https://msdn.microsoft.com/en-us/library/system.web.httprequest.form(v=vs.110).aspx), [Request.Cookies](https://msdn.microsoft.com/en-us/library/system.web.httprequest.cookies(v=vs.110).aspx) and [Request.ServerVariables](https://msdn.microsoft.com/en-us/library/system.web.httprequest.servervariables(v=vs.110).aspx) collections.
- Never change state via a GET request and always check the Request type using [HttpRequest.HttpMethod](https://msdn.microsoft.com/en-us/library/system.web.httprequest.httpmethod(v=vs.110).aspx).
- To mitigate [Cross-Site Request Forgery (CSRF)](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF)) attack, one method is to add a token to every form, which is verified when the form is submitted.  This process can be automated by implementing an [HTTP module](https://msdn.microsoft.com/en-us/library/bb398986(v=vs.100).aspx).  [AntiCSRF - A Cross Site Request Forgery (CSRF) module for ASP.NET](https://anticsrf.codeplex.com/) is a good example of this.
- Do not disable [Event Validation](https://msdn.microsoft.com/en-us/library/system.web.ui.page.enableeventvalidation(v=vs.110).aspx) as they prevent the falsification of events.
- Do not rely on the [Request Headers](http://www.w3.org/Protocols/HTTP/HTRQ_Headers.html) as they can be easily faked, most notably the [Referer](http://www.w3.org/Protocols/HTTP/HTRQ_Headers.html#z14) Header.
- Do not disable [system.web/httpRuntime, attribute enableHeaderChecking](https://msdn.microsoft.com/en-CA/library/e1f13641(v=vs.100).aspx) in web.config or in code using [HttpRuntimeSection.EnableHeaderChecking Property](https://msdn.microsoft.com/en-us/library/system.web.configuration.httpruntimesection.enableheaderchecking(v=vs.110).aspx).




