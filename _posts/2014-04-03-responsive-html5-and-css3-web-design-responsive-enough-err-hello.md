---
title: "Responsive HTML5 and CSS3 Web Design: Responsive Enough? Err… Hello?!?"
date: "2014-04-03"
categories: 
  - "web-design"
---

[![ResponsiveEnough](/technical-blog/assets/images/responsiveenough.jpg)](http://rodansotto.files.wordpress.com/2014/04/responsiveenough.jpg)Looking at the figure above, it would be nice if the web site displays properly in other browser sizes from other devices.  Well have no fear, responsive web design is here.

So what is responsive web design?  Responsive web design was coined by [Ethan Marcotte](http://www.alistapart.com/articles/responsive-web-design/).  It is basically an approach to making web sites respond to the differing viewports of browsers on different devices by using 3 existing techniques:

- flexible grid layout,
- flexible images, and
- media and media queries.

One should design for the smallest viewport first then enhance for larger viewports.

If you visit this site, [http://mediaqueri.es/](http://mediaqueri.es/ "http://mediaqueri.es/"), you will see how responsive web sites look or display at the different design “break points”.  Try one of the sites there and see for yourself by changing the browser size.

Some tools to resize your browser quickly:

- In IE9, use the Developer Toolbar and go to Tools –> Resize.
- In Chrome, you can use the Developer Toolbar too but this is to emulate a device.  You go to the Emulation Panel beside the Console panel, after showing the console. See [Mobile Emulation](https://developers.google.com/chrome-developer-tools/docs/mobile-emulation).
- Alternatively, you can use a Chrome browser extension [Resolution Test](https://chrome.google.com/webstore/detail/resolution-test/idhfcdbheobinplaamokffboaccidbal).

So how do HTML5 and CSS3 help in making web sites responsive?  The following are some of the features in HTML5 and CSS3, just to give you an idea.

_For HTML5:_

- Streamlined markup and more meaningful semantic elements provide for a leaner and faster-loading code base.
- Feedback to user on form submissions negates the need for more resource heavy JavaScript form processing.
- _<header><nav>_ replaces your usual _<div class=”navigation”>_ section.

_For CSS3:_

- Use of relative measurement units (i.e. em or ems and percentages) instead of pixels.
- Media queries that targets specific CSS rules at specific viewports.
- _border-radius_ property and _background-image linear-gradient_ property that allow for a rounded button with gradient background image without actually using any images.
- 3D transformations that make animation lightweight, maintainable, and perfect for a responsive design, although IE9 does not support this.
- In essence, CSS3’s media queries, modules, gradients, shadows, typography, animations, and transformations pushes responsive design even further.
- Check this site, [http://www.csszengarden.com/](http://www.csszengarden.com/ "http://www.csszengarden.com/").  It demonstrates what can be accomplished through CSS-based design.

This is just the first in a series of posts on responsive web design using HTML5 and CSS3.  Next I’ll go into more details and more examples.
