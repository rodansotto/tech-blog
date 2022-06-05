---
title: "My notes on Angular (2.0+)"
date: "2017-11-23"
categories: 
  - "javascript"
---

![]({{ site.baseurl }}/assets/images/angularbloglogo1.png)I've been following Angular for a while now and decided recently to develop Angular 2.0+ applications (skipped the previous version, AngularJS, as it's totally different)

.  My initial impression: it does make developing SPA easy and opens the door to the world of open-source frameworks and libraries.  So here are some notes I gathered.

- An angular application is composed of one or more modules (see [NgModules](https://angular.io/guide/ngmodule) and [Bootstrapping](https://angular.io/guide/bootstrapping)).  It has one root module and any number of feature modules.
- An angular module contains one or more components (see [@Component](https://angular.io/api/core/Component)).
- An angular component is comprised of a template (the view), class (the data) and metadata ([this](https://angular.io/tutorial/toh-pt1#create-the-heroes-component) is what an angular component code looks like).
- An angular [template](https://angular.io/guide/template-syntax) represents the view and displays data.  Use [interpolation](https://angular.io/guide/template-syntax#interpolation----) to bind data and the [common built-in structural directives](https://angular.io/guide/template-syntax#built-in-structural-directives) to shape/reshape the DOM's structure. See [Structural Directives](https://angular.io/guide/structural-directives) to learn more about them.
- Other types of data binding are: [property binding](https://angular.io/guide/template-syntax#property-binding--property-), [event binding](https://angular.io/guide/template-syntax#event-binding---event-), and [two-way binding](https://angular.io/guide/template-syntax#two-way-binding---), the banana in a box ;).
- To edit, transform or format the data binded to the view, angular [pipes](https://angular.io/guide/pipes) are used.  Angular comes with [built-in pipes](https://angular.io/guide/pipes#built-in-pipes) but [custom pipes](https://angular.io/guide/pipes#custom-pipes) can be created.
- Angular provides [lifecycle hooks](https://angular.io/guide/lifecycle-hooks) for the component to act on, much like event-driven programming.
- More than one components can make up the UI.  These components can be separate components, or nested components - components that are inside another component, also called shared components.
- Any component can be nested in a container component by using the nested component's directive (the component's selector property) in the container's template.
- Angular provides interactions between components where information between components need to be shared.  Use the [Input decorator](https://angular.io/guide/component-interaction#pass-data-from-parent-to-child-with-input-binding) to pass data from parent to child via property binding.  Use the [Output decorator](https://angular.io/guide/component-interaction#parent-listens-for-child-event) to pass data from child to parent via event binding.  See [Component Interaction](https://angular.io/guide/component-interaction#component-interaction) for more information.
- Angular components contain logic to support the view.  For any other logic that is not tied to the view, they are usually declared as angular services (or service providers), well technically speaking declared as [@Injectable](https://angular.io/guide/dependency-injection#injectable), because they are injected to components that need them.  Services created need to be registered first before injected.  See [Angular Dependency Injection](https://angular.io/guide/dependency-injection#angular-dependency-injection) for more details.
- [HttpClient](https://angular.io/guide/http#httpclient) is one of the built-in services in Angular used to communicate over HTTP.  Since calls to HttpClient is asynchronous, the caller needs to subscribe to an [observable](http://reactivex.io/documentation/observable.html).  Angular uses [Reactive Extensions Library](http://reactivex.io/) for this.
- To implement navigation from one view to the next, angular routers are used.  The basics require 1) [configuring the routes](https://angular.io/guide/router#configuration) where the path and the component (or view) to go to are specified, 2) adding the [router outlet](https://angular.io/guide/router#router-outlet) to the host view's HTML where the routed views are placed, and 3) adding the [router links](https://angular.io/guide/router#router-links) usually on anchor tag clicks.
- Parameters can be passed to a route by configuring a [route with a parameter](https://angular.io/guide/router#route-definition-with-a-parameter), and [setting the the route parameters in the view](https://angular.io/guide/router#setting-the-route-parameters-in-the-list-view) using the [link parameters array](https://angular.io/guide/router#appendix-link-parameters-array).
- To activate route in code, use the router service injected to the component and call it's navigate method ([this](https://angular.io/guide/router#query-parameters-and-fragments) shows how to activate route in code).
- In cases where a check needs to be made or some work needs to be done before routing, use [angular route guards](https://angular.io/guide/router#milestone-5-route-guards).  Basically create a service (an injectable class) that implements CanActivate and update the configured routes with a canActivate property that references it.
- [Routing and Navigation](https://angular.io/guide/router#routing--navigation) contains the complete information on this topic.

 

**Resource Links:**

- [Angular Docs](https://angular.io/docs)
- [npm Docs](https://docs.npmjs.com/)
- [Angular CLI Wiki](https://github.com/angular/angular-cli/wiki)
- [TypeScript Docs](https://www.typescriptlang.org/docs/home.html)
