---
title: "General: If we have Cloud, then what is SaaS? What about ASP?"
date: "2013-04-18"
categories: 
  - "general"
---

I was going through some job description that I was applying for and stumbled upon this tech jargon **multi-tenant** describing a data architecture, which I will be talking about on a separate post under SQL Server.  I searched the Internet and found out that this tech jargon is actually common in the **SaaS**, **Cloud** or **ASP** space.  From my limited understanding, these spaces deal, in one way or the other, with delivering software as a service.  As it turned out, multi-tenant means serving multiple clients or tenants and that makes logical sense when talking about these spaces.  But now I wonder, is there any difference between these spaces.

**ASP** stands for **Application Service Provider**.   So it's actually a company that specializes in providing software as a service.  An ASP runs or hosts applications on behalf of the clients.  The clients pay or subscribe for that service.  How this software is delivered to the clients is what differentiates one from another ASP.  These ASPs initially delivered software through virtualization and for some client-server applications, the client side components of the application are installed on the users' computers.  Nowadays, with Internet technologies, these applications are now delivered through browsers with no need for any installation on the users' computers.

**SaaS** stands for **Software as a Service**.  So this is a type of software delivery model used by ASPs.  In an ideal situation, the application being provided to the clients is a multi-tenant application -  only  one running application servicing multiple clients or tenants.  Other ASPs employ a multi-instance application - for each client or group of clients, an instance of the application is running, thus multiple applications are serving multiple clients.

**Cloud** does not stand for anything.  If talking to non-technical people, it would make more sense to say **Cloud Computing**.  Cloud is more than SaaS.  In fact SaaS is just one type of service provided by Cloud.  Cloud is basically where one would go to use a computing resource that is delivered over a network, much like a SaaS.  But it's not only software that is available in Cloud.  In fact, Cloud also provides the following types of services: **IaaS** (**Infrastructure as a Service**), **PaaS** (**Platform as a Service**), and **NaaS** (**Network as a Service**).

Hopefully this clears up some confusion.  I have not provided enough description but enough to get one in the right direction.  As always, Internet is the best resource if you need to dig further in these technologies.

EDIT: [How Cloud Computing Works](http://computer.howstuffworks.com/cloud-computing/cloud-computing.htm) explains what "cloud" is all about.
