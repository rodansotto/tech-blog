---
title: "HTTP Fundamentals, Part 2: Communication Stack, HTTP Connections, and REST Style of Architecture"
date: "2014-02-05"
categories: 
  - "web-design"
---

**Communication Stack**

**HTTP** is the topmost layer in the communication stack and is called an application layer protocol.  From the web browser, it travels down a series of layers, and when it arrives at the web server, it then travels up through a series of layers.  The layers that make up the communication stack are:

- **Application** – An example would be **HTTP**.
- **Transport** – Responsible for error detection, flow control, and overall reliability.  An example would be **TCP (Transmission Control Protocol)**.
- **Network** – Responsible for taking pieces of information and moving them through the various switches, routers, gateways, repeaters, and other devices that move information from one network to the next and all around the world.  An example would be **IP (Internet Protocol)**.  This is where the **IP address** comes in to play.
- **Data Link** – This is where data have to travel over a piece of wire, a fibre optic cable, a wireless network, or a satellite link.  It’s focused more on 1s, 0s, and electric signals.  An example would be **Ethernet**.

**HTTP** relies on **TCP** to connect to the server.  It opens a **TCP socket** by specifying the **server address** (host name) and **port** (defaults to 80).  With an open socket, HTTP can write into it and read from it when it gets response from the server.

A free tool you can use to view HTTP,  TCP and IP packets is [**Wireshark**](http://www.wireshark.org/).

 

**HTTP Connections**

Gone is the old days of simple web pages.  Nowadays, a webpage requires more than a single resource to fully render.  To compensate for this and so as not to bog down the Internet, several approaches have been employed   when using HTTP:

- **Parallel Connections** – Browsers can open more than one connection to download several resources at the same time but there is a limit to it that is set by the server.  This is better though than doing a request in a serial one-by-one fashion.
- **Persistent Connections** – Browsers can persist a connection to the server reducing overhead associated with opening and closing a TCP socket and thus improving performance.  **This is the default connection style with HTTP 1.1**.  These connections are only persistent for a period of time as set by either the server or the browser.  The server can also opt not to accept a persistent connection by specifying the **Connection: close** header in every HTTP response message.
- **Pipelined Connections** – Not widely used as parallel and persistent connections, this type of connection allow multiple requests to be sent by the browser before the browser waits for the first response.

 

**REST Style of Architecture**

**HTTP** lends itself to the **[REpresentational State Transfer (REST)](http://en.wikipedia.org/wiki/Representational_state_transfer)** style of architecture.  If you think of resources and URLs as just not files on a web server’s file system, but more like as resource abstractions, you start to see the web as part of your application and as a flexible architectural layer you can build on.  The following are some **RESTful** aspects of a URL:

- A URL cannot restrict the client or server to a specific type of technology.
- A URL cannot force the server to store a resource using any particular technology.
- A URL cannot specify the representation of a specific resource, and a resource can have multiple representations.  This is where content negotiation, discussed in [**Part 1**](http://rodansotto.wordpress.com/2013/10/29/http-fundamentals-part-1-url-encoding-request-and-response/) of this series, kicks in.
- A URL cannot say what a user wants to do with a resource.  This is where the HTTP methods comes in.

Because an **HTTP message** is a **simple**, **plain text message** and **fully self-describing**, and together with the **indirection provided by URLs**, HTTP applications can rely on a number of **services that provide value** as a message moves between the client application and the server application.  Examples of services would be:

- **Web server**
    - Route message to proper application
    - Log message to a local file
    - Compress message if client supports it
- **Proxy server** – A computer that sits between a client and server.  Can either be a **forward proxy** that sits closer to the client or a **reverse proxy** that sits closer to the server.  Note that a proxy server does not have to be a physical server.
    - Prevent message to go out to specific servers
    - Remove confidential data in the message
    - Log message to create audit trails
    - Compress message
    - Forward message to one of several web servers (load balancing)
    - Encrypt and decrypt message (SSL acceleration)
    - Filter out potentially dangerous message (cross-site scripting, SQL injection attack)
    - Store copies of frequently accessed resources and respond to messages requesting those resources directly (caching)

These services can be layered into the network without impacting the application, and that is the beauty of HTTP.  It is scalable, simple, reliable, and loosely coupled.  In fact, **REST was initially described in the context of HTTP**.

 

\*This article is Part 2 of the HTTP Fundamental series.  For Part 1, click [**here**](http://rodansotto.wordpress.com/2013/10/29/http-fundamentals-part-1-url-encoding-request-and-response/).
