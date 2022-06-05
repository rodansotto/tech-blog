---
title: "Product Catalog: An Angular and Material Demo"
date: "2017-12-04"
categories: 
  - "javascript"
---

![]({{ site.baseurl }}/assets/images/productcatalogangulardemob.jpg)

[DEMO](http://rodansotto.com/projects/angular/productcatalogdemo/#/products) | CODE (will put it up soon!)



This is my first Angular app but not the first time creating the product list for the AdventureWorks products database.  I previously created one using MVC 4 (check my post [here](https://rodansotto.wordpress.com/2015/10/19/a-custom-webgrid-my-1st-iteration/)) but this time around it has an image view besides the list view and it uses Web API to communicate to the back-end.  I initially used Bootstrap as my UI framework but decided to use Angular Material as I found it to be more easy to integrate with Angular.

It was an adventure and really worth going through it.  I was thinking of using VS Code but when I tried it hoping it should be similar to the full-featured VS IDE but it's not.  Since I don't want to spend another time familiarizing myself with VS Code, I went with VS IDE, for now.

So how did I make VS IDE work?  Well I only used VS IDE as a glorified editor really.  I depended on angular CLI pretty much for generating my initial angular app and scaffolding.  With VS IDE, I created a blank ASP.NET application and just opened my angular app files from there.

In this first iteration, I only have one module and one component that displays the product catalog.  I did setup a route for the component.  As I refactor and/or improve on this app, it will eventually have a proper navigation.  And of course, I had to rewrite rules for the URL so it uses the main angular app's base href.

I have an angular service that calls a web API to retrieve the products data.  I had to pass some paging, sorting, and search info to the web API and I thought I can pass them in the request body but unfortunately Angular's HttpClient does not allow it so I ended up passing them as URL parameters.  I only have one web API method on the backed.  And I only request for {{ site.baseurl }}/assets/images/photos if the image view is active.

There is not much code on the component side that really needs explanation, it's pretty straightforward.  Much of the effort is in making the angular material components work.  For this app, I used the following angular material components: table, paginator, sort, input, button, icon, card, tooltip, and progress spinner.  I really enjoy working on UI so this was worth the time and I think it's a good UI and good thing I went for angular material.

So what's next?  I still have to do the product detail view.  As for long-term goal, I am thinking of making this an angular module that you can just plug in in your projects, maybe thinking of creating an angular product catalog and ordering module, something like that.  Also might add in some product management module.

 

**Additional Resources:**

- [Angular Material](https://material.angular.io/)
- [Material Design Icons](https://material.io/icons/)
