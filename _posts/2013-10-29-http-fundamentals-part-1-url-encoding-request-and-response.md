---
title: "HTTP Fundamentals, Part 1: URL, Encoding, Request and Response"
date: "2013-10-29"
categories: 
  - "web-design"
---

HTTP fundamentals a web developer needs to know:

- **HTTP address** is called a **URL** (**Uniform Resource Locator**). Everything on the Internet is a resource.
    
     
    
    Example: http://mydevsite:1234/mydevpage?first=Rodan&last=Sotto#comment
    
     
    
    **URL** consists of the following parts:
    
     
    
    <scheme\>://<host\>:<port\>/<path\>?<query\>#<fragment\>
    
     
    
    - **Scheme** describes how to access a particular resource. In our example above, it’s **HTTP**. It can be **HTTPS**, **FTP**, or **MAILTO**.
    - **Host** is the name of the computer hosting the resource. In our example, it’s **mydevsite**.
    - **Path** is the path to the specific resource. In our example, it’s **/mydevpage**. A **URL** does not have to point to a specific file, like an image (**\*.jpg**) or **ASPX** file (**\*.aspx**). Nowadays, URLs are dynamic and, for **search engine optimization** (**SEO**), they usually contain descriptive keywords. See [**URL optimization for SEO**](http://blog.woorank.com/2013/05/url-optimization-5-best-practices-for-seo/)_._
    - **Port** is specified if the host is listening to **HTTP requests** on a port number other than **80**, which is the **default HTTP port number**. Usually specified when testing, debugging, or developing web sites. In our example, its **1234**.
    - **Query**, or **query string**, comes after **?** (the **question mark**) and contains **name=value** pairs separated by **&** (the ampersand). In our example, its **first=Rodan&last=Sotto**.
    - **Fragment** is the part after the **#** sign. This is processed by the browser to display the element identified by the fragment at the top of the screen. In our example, the **comment** section is displayed on top of the screen.

- **URL encoding** is the process of encoding unsafe characters found in the URL. The Internet standards list characters that are unsafe for URLs and thus they are encoded using **%** (the percent sign). One unsafe character is the space character and is usually encoded to **%20**. See [**URL unsafe characters**](http://www.blooberry.com/indexdot/html/topics/urlencoding.htm).
    
     
    
    Example: http://mydevsite:1234/mydevpage/my%20file.txt
    
     
    
- **Content type** is the **MIME** (**Multipurpose Internet Mail Extensions**) type that the server sends to the client so the requested resource can be displayed properly. The content type for an HTML resource, for example, is **“text/html”**, where **“text”** is the primary media type and **“html”** is the media subtype. If the client did not receive any content type information, it can guess the content type by scanning the first bytes of the response, and if that fails, will use the **file extension** instead. The client can also specify which content types it will accept when requesting a resource with multiple representations, a process called **content type negotiation**.

- **HTTP request** and **HTTP response** form a **single HTTP transaction**. These 2 different message types are carefully formatted readable text messages that both server and client understand. Anyone that can send data over a network can participate, like the good old command line **Telnet**. Tools, such as **Fiddler**, can be used to inspect HTTP messages.

- **HTTP Request Methods**:
    - **GET** to retrieve a resource
    - **PUT** to store a resource
    - **DELETE** to remove a resource
    - **POST** to update a resource
    - **HEAD** to retrieve the headers for a resource

- **Redirect** response is sent by the server to the client to mean that the resource has moved to a new location and the client needs to send a request again to the new location. **Redirect** is also used to make sure all requests for resources from a server go through a specific location, a **SEO** practice known as **[URL canonicalization](http://www.mattcutts.com/blog/seo-advice-url-canonicalization/)**.

- **POST/Redirect/GET** pattern is a common web design pattern employed by web applications when servicing POST requests so that the client is left with a response from a GET request. This avoids the issues with user refreshing or printing the page as a result of of the response of a POST request.

- 3 common types of HTTP requests:
    - **GET request** , for example when clicking a link.
        
         
        
        GET http://mydevsite:1234/mydevpage/mydefault.aspx HTTP/1.1
        Host: mydevsite.com
        
         
        
    - **POST request**, when filling up a form whose method is POST. Form inputs go into the HTTP message body.
        
         
        
        POST http://mydevsite:1234/mydevpage HTTP/1.1
        Host: mydevsite.com
        firstName=Rodan&lastName=Sotto
        
         
        
    - **Forms and GET request**, when filling up a form whose method is GET. Form inputs go into the query string of the URL. Use this type of request if the operation does not require writing to the server, basically a safe retrieval operation. An example would be a search.
        
         
        
        GET http://mydevsite:1234/mydevpage?first=Rodan&last=Sotto HTTP/1.1
        Host: mydevsite.com
        
         
        
- **HTTP request message** consists of the following parts:
    
     
    
    \[method\] \[URL\] \[version\]
    \[headers\]
    \[body\]
    
     
    
- **HTTP request headers**, the **Host** header is one of them, contain useful information that can help the server process a request. Except for the host header, all request headers are optional. Popular request headers are:
    - **Referer** – URL of the referring page
    - **User-Agent** – information on the client software making the request, usually the browser
    - **Accept** – content types the client is willing to accept; used for content type negotiation
    - **Accept-Language** – languages the client prefers
    - **Cookie** – cookie information
    - **If-Modified-Since** – date the client last retrieved the resource; requests the server to only send the resource if it’s been modified since that time

- A **full HTTP request** might look like the one below. Note that some headers contain multiple values, like the Accept header. The **\*** (asterisk) in one of the values, usually provided as the last value, means anything. The **q=\[0..1\]** represents relative degree of preference, 1.0 being the highest and the default value. In our example below, the Accept header tells us the client will accept any content types but likes HTML best.
    
     
    
    GET http://mydevsite/ HTTP/1.1
    Host: mydevsite.com
    Connection: keep-alive
    User-Agent: Mozilla/5.0 (Windows NT 6.1; WOW64) Chrome/16.0.912.75 Safari/535.7
    Accept: text/html,application/xhtml+xml,application/xml;q=0.9,\*/\*;q=0.8
    Referer: http://www.google.com/url?&q=mydevsite
    Accept-Encoding: gzip,deflate,sdch
    Accept-Language: en-US,en;q=0.8
    Accept-Charset: ISO-8859-1,utf-8;q=0.7,\*;q=0.3
    
     
    
- **HTTP response message** consists of the following parts:
    
     
    
    \[version\] \[status\] \[reason\]
    \[headers\]
    \[body\]
    
     
    
- A **full HTTP response** might look like the one below:
    
     
    
    HTTP/1.1 200 OK
    Cache-Control: private
    Content-Type: text/html; charset=utf-8
    Server: Microsoft-IIS/7.0
    X-AspNet-Version: 2.0.50727
    X-Powered-By: ASP.NET
    Date: Sat, 14 Jan 2012 04:00:08 GMT
    Connection: close
    Content-Length: 17151
    <html\>
    <head\>
    <title\>My Development Site</title\>
    </head\>
    <body\>
    ... content ...
    </body\>
    </html\>
    
     
    
- **HTTP Response Status Code Categories**
    - 100-199 – **Informational**
    - 200-299 – **Successful**
    - 300-399 – **Redirection**
    - 400-499 – **Client Error**
    - 500-599 – **Server Error**

- **Common HTTP Response Status Codes**
    - **200** – OK
    - **301** – Moved Permanently; redirect response used in URL canonicalization
    - **302** – Moved Temporarily; redirect response used in the POST/Redirect/GET pattern
    - **304** – Not Modified; in response to the If-Modified-Since request header
    - **400** – Bad Request
    - **403** – Forbidden
    - **404** – Not Found
    - **500** – Internal Server Error; usually happens due to programming errors in a web application
