---
title: ".NET 3.5: Quick look at what is in WCF"
date: "2009-04-18"
categories: 
  - "net"
---

**Windows Communication Foundation (WCF)** is a platform for building service-oriented applications.  The following are some of the highlights in WCF:

- Defines the following three core contracts with its consumers when creating WCF services: **Service contract**, **Data contract**, and **Message contract**.
- Use of **service endpoint** to expose WCF services to consumers.
- Availability of various service hosting applications: managed application such as **Console application**, **Windows service**, or **Windows Forms application**, Web server using **IIS** or **Windows Process Activation Service (WAS)**.  **WAS** also supports non-**HTTP** protocols such as **TCP**, **MSMQ**, and **named pipes**.  Also available is the WCF-provided host (**wcfSvcHost.exe**).
