---
title: "Some Visual Studio Productivity Tips"
date: "2017-11-09"
categories: 
  - "asp-net-mvc"
---

![]({{ site.baseurl }}/assets/images/vsbloglogo.png)



- Use [Browser Link](https://docs.microsoft.com/en-us/aspnet/visual-studio/overview/2013/using-browser-link) which uses SignalR to refresh browsers linked to your project.
- [Create your own Scaffolded Item](https://stackoverflow.com/questions/20037365/how-to-create-custom-scaffold-templates-in-asp-net-mvc5).  When you _Add -> New Item..._, there is also option _New Scaffolded Item...._  You can add your new scaffolded item as one of the options.  You can copy and modify existing scaffolded items found at _C:\\Program Files (x86)\\Microsoft Visual Studio\\2017\\Enterprise\\Common7\\IDE\\Extensions\\Microsoft\\Web\\Mvc\\Scaffolding\\Templates_ _(for Visual Studio 2017)_.  Copy folder you want to modify and paste it under _CodeTemplates_ folder under your project root.  Make sure names of folders/files are intact so Visual Studio can pick them up.
- Install [Web Essentials](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.WebExtensionPack2017) extensions which provides the ultimate web development experience, such as the Browser Reload on Save, CSS Tools, HTML Tools, and ZenCoding.  Note that the design and inspect modes under Browser Link for Visual Studio 2017 is missing so you will need to download a separate extension for this, the [Browser Link Inspector](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.BrowserLinkInspector2017).
- Use [Visual Studio shortcut keys](http://visualstudioshortcuts.com/2017/), such as Alt+1 and Shift+Alt+W.
- Use _'&'_ intellisense to insert character entities on html/razor pages, as well as intellisense on bootstrap _'data-'_ attributes, on angular directives _'ng-'_, on angular templates or handle bars, and on web.config rewrite rules.
- Use CSS editor tricks such as hover on CSS property to show browser support matrix.
- Use [LESS](http://lesscss.org/#) which extends CSS with features such as variables, mixins, and nested rules.
- Install [SideWaffle](http://sidewaffle.com/) extension which provides useful snippets, project and item templates.  Unfortunately as of the time of this post, Visual Studio 2017 version is still under development.
