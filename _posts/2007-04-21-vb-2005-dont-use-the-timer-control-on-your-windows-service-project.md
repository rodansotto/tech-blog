---
title: "VB 2005: Don't use the Timer control on your Windows Service project"
date: "2007-04-21"
categories: 
  - "vb-net"
---

Just wasted my time trying to debug why the **Timer control** (from the **Toolbox** under **Components**) on my Windows Service project was not working at all.  Then I tried explicitly creating a **Timer object** from the **System.Timers.Timer** class and now it is working.

One thing I noticed though is that when I used the Timer control, the event that is fired when the interval has elapsed is the **Tick** event while when I used the Timer object from the System.Timers.Timer class, the event fired is the **Elapsed** event.  Found out that they are different because the Timer control is created from the **System.Windows.Forms.Timer** class.
