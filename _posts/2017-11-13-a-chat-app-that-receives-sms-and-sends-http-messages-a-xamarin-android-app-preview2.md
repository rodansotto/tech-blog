---
title: "A chat app that receives SMS and sends HTTP messages (A Xamarin Android App Preview)"
date: "2017-11-13"
categories: 
  - "android"
---

[PREVIEW](https://rodansotto.github.io/projects/mysmswebchatpreview.html)

![MySMSWebChat02]({{ site.baseurl }}/assets/images/mysmswebchat021.jpg)A while back, I delved into Android development using Android Studio and Java (in this [article](https://rodansotto.github.io/tech-blog/2014/03/18/android-development-main-method-application-lifecycle-and-event-handling.html)).  It was a little bit difficult for me as I need to familiarize myself with Android Studio and relearn Java.  But with Xamarin now part of Visual Studio, it became easier.  All I need to concern myself is the Android development itself.  So in just a few days, I created my first usable Android mobile application.  This app can now receive SMS messages but the sending of HTTP messages is still in the works (which is why it's still in a preview).

Anyways, what did I do to make this SMS work?  The app registers a broadcast receiver for SMS messages.  This broadcast receiver then sends an ordered broadcast to the app where it has 2 more broadcast receivers: one broadcast receiver to update the UI with the SMS message received when the app is running, and another one to display a notification when the app is not running.  When the notification is clicked, the app will launch and the chat will start.

I see a potential in this mobile development space for me, and for this app which I will continually build on.  There are still a lot of work in progress here.  One takeaway for me on this is that Xamarin does really help you develop Android apps using your favorite language C# and your favorite IDE Visual Studio.

**Resources and Tools:**

- [Xamarin.Android Guides](https://developer.xamarin.com/guides/android/)
- [Android Developer Guides](https://developer.android.com/develop/index.html)
- [Android Asset Studio](https://romannurik.github.io/AndroidAssetStudio/index.html)
- [Material Design](https://material.io/)
- [Color Wheel Calculator From Sessions College](https://www.sessions.edu/color-calculator/)
- [Iconshock](https://www.iconshock.com/)
- [SendaText - Free SMS Messages](https://www.sendatext.co/Canada)
- [Android Device Art Generator](https://developer.android.com/distribute/marketing-tools/device-art-generator.html)
