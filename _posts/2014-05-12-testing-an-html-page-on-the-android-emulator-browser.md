---
title: "Testing an HTML Page on the Android Emulator Browser"
date: "2014-05-12"
categories: 
  - "android"
---

[![HTMLonAndroid](/technical-blog/assets/images/htmlonandroid.jpg)](http://rodansotto.files.wordpress.com/2014/05/htmlonandroid.jpg)Although you can easily test your HTML page’s responsive design using Chrome’s [Mobile Emulation](https://developers.google.com/chrome-developer-tools/docs/mobile-emulation) feature, you can also do it, albeit the harder way, by loading the page on the Android emulator’s browser.

First you must run the **Android Virtual Device (AVD) Manager** to launch your Android emulator.  You don’t necessarily have to run the IDE that came with your Android emulator (e.g. Eclipse or Android Studio).  You can use the batch file **android.bat** which you can find under **sdk/tools** of your Android installation folder.  In the **command prompt**, just type in **“android.bat avd”**.

Once you have the AVD manager running, select the device you want to emulate.  But before starting the device, make sure you have specified a size for the **SD card**, as we will be using this to store the HTML page.  **2GB** should be OK.

Next, you need to copy the HTML page from the computer to the Android emulator’s SD card storage using the **Android Debug Bridge** program or **adb.exe**, which you can find under **sdk/platform-tools**.  Using a command prompt, run adb with the following options:

- **“adb devices”** which will list the devices attached including the emulator ones.  To connect to the emulator you just started, you need to get the **device number** assigned to the emulator from the device list.  Or you can get the number from the emulator window bar.
- **“adb connect localhost:_5554”_** which will connect you to the device emulator.   The number **_5554_** should be replaced with the device number for your emulator.
- **“adb push C:\\YourFolder\\YourHTMLPage.html sdcard/.”**  which will copy your HTML page from your computer’s local folder to the Android emulator’s **sdcard** folder.  Note that the Android OS is based on Linux kernel which is why the destination path follows the Linux syntax.
- **“adb shell”** which will bring you to the Android emulator file system.  You can go to the SD card folder to check if your HTML page was copied successfully by entering **“cd sdcard”** and then **“ls –al”**.  It’s exactly a Linux file system at your fingertip.  If you want to create a folder under the SD card folder you can use **mkdir**.  To get out of the shell, just type in **exit**.

You can also copy any accompanying CSS and JavaScript files for the HTML page you just copied.

Now you are ready to view the HTML page on the Android emulator browser.  On the emulator, open up the browser and type in the URL [**file:///sdcard/YourHTMLPage.html**]($YourHTMLPage.html) on the address window.

Note that by default, these mobile browsers will automatically shrink the page to fit the mobile device width.  The following meta tag should be used to override this and display the page at 100 percent.

<meta name\="viewport" content\="width=device-width,initial-scale=1.0"/>
