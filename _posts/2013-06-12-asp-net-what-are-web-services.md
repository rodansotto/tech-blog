---
title: "ASP.NET: What are web services?"
date: "2013-06-12"
categories: 
  - "asp-net"
---

- **Web services** are services provided over the web using standard technologies such as **XML**, a **W3C** standard.
- Any application on any platform can consume a web service as long as it is able to understand XML.
- XML is text based, thus it is quick and easy to download and even easier to use.
- To consume an **ASP.NET web service**, look for an **.asmx** file.
- An example of a web service is [http://www.webservicex.net/ConvertTemperature.asmx](http://www.webservicex.net/ConvertTemperature.asmx).
- There are **3 methods** used to communicate with a web service: **HTTP-GET**, **HTTP-POST**, and **SOAP**.
- In **HTTP GET** and **POST**, the response body is an XML.  Below is an example response from the **ConvertTemperature** web service mentioned above, converting 21.5 degrees Celcius to degrees Farenheit.
    
    <?xml version\="1.0" encoding\="UTF-8"?\>
    <double xmlns\="http://www.webserviceX.NET/"\>70.7</double\>
    
     
    

 

- **SOAP** (**Simple Object Access Protocol**) is basically a well-formed XML created just for the purpose of sending requests and receiving responses to and from the web service.
- A **SOAP request** is wrapped in an **HTTP-POST**.  The example below is the SOAP request sent to the ConvertTemperature web service, separated into a request header and request body:
    
    POST /ConvertTemperature.asmx HTTP/1.1
    Host: www.webservicex.net
    Content-Type: text/xml; charset=utf-8
    Content-Length: \[length\]
    SOAPAction: "http://www.webserviceX.NET/ConvertTemp"
    
     
    
    <?xml version\="1.0" encoding\="utf-8"?\>
    <soap:Envelope xmlns:xsi\="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd\="http://www.w3.org/2001/XMLSchema" xmlns:soap\="http://schemas.xmlsoap.org/soap/envelope/"\>
      <soap:Body\>
        <ConvertTemp xmlns\="http://www.webserviceX.NET/"\>
          <Temperature\>21.5</Temperature\>
          <FromUnit\>degreeCelsius</FromUnit\>
          <ToUnit\>degreeFahrenheit</ToUnit\>
        </ConvertTemp\>
      </soap:Body\>
    </soap:Envelope\>
    
     
    

 

- The corresponding **SOAP** response is below (response header not shown):
    
    <?xml version\="1.0" encoding\="utf-8"?\>
    <soap:Envelope xmlns:xsi\="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd\="http://www.w3.org/2001/XMLSchema" xmlns:soap\="http://schemas.xmlsoap.org/soap/envelope/"\>
      <soap:Body\>
        <ConvertTempResponse xmlns\="http://www.webserviceX.NET/"\>
          <ConvertTempResult\>70.7</ConvertTempResult\>
        </ConvertTempResponse\>
      </soap:Body\>
    </soap:Envelope\>
    
     
    

 

- In the SOAP request and response body, you need to have at the minimum the SOAP tags **<Envelope>** and **<Body>**.  You can also have the optional SOAP tag **<Header>**.  Inside the **<Body>** SOAP tag contains other tags that are specific to the web service.

 

In my next post, I will talk about what is required to create a web service in ASP.NET.
