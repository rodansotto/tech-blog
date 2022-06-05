---
title: "JavaScript: You think you know it well?"
date: "2014-02-13"
categories: 
  - "javascript"
---

Just because you are a C# or Java developer that you think you know JavaScript well.  Well I don’t.  But no worries, below are some quick pointers to remember:

- _null_ and _undefined_ are types, just like Numbers, Strings, Booleans, and Objects.  _null_ indicates a deliberate non-value while _undefined_ indicates an uninitialized value.
- Primitive/literal values (_null_, _undefined_, _“string”_, _10_, _true_, _false_) are converted to objects (wrapper objects) when properties are accessed.
- Functions and Arrays are special types of objects.
- Built in Error types are there as well.
- _Object()_, _Array()_, _String()_, _Number()_, _Boolean()_, _Function()_, _Date()_, _RegExp()_, and _Error()_ are native constructor functions.
- _parseInt()_ and _parseFloat()_ parse the number in string until it reaches an invalid character.
- Unary + operator converts values to numbers (_\+ “42” = 42_ ) and returns _NaN_ (Not a Number) if non-numeric.
- _isNaN()_ tests for _NaN_.
- _isFinite()_ tests for Infinity (1/0), -Infinity (-1/0), and _NaN_.
- _false_, _0_, empty string (_""_ ), _NaN_, _null_, and _undefined_ convert to false, and all others convert to true.
- Blocks do not have scope, only functions have scope.
- _"3" + 4 + 5 = 345_, while _3 + 4 + "5" = 75_.
- Triple-equals operator avoids type coercion.  _1 === true_ is false, but _true === true_ is true.
- JavaScript objects are simple collections of name-value pairs where the name is a JavaScript string and the value is any JavaScript value.
- _array.length_ isn’t necessarily the number of items in the array.  It is one more than the highest index.
- No _return_ statement or empty return with no value in a function returns _undefined_.
- _arguments_ variable contains all the values passed to the function.
- IIFEs (Immediately Invoked Function Expressions) is basically what it says.  It’s a function in an expression and invoked immediately ( _(function () { … })();_  )
- To call functions recursively, you can use a named IIFE ( _(function myFunc() { myFunc(); })();_  ).  The name is only available to the function’s own scope.
- _this_ inside a function refers to the current object if the function is called against an object or using dot notation or bracket notation; otherwise it will refer to the global object.
- Global object or the head object in JavaScript in a web browser environment is the _window_ object.  Variables you declare globally in your JavaScript code will become properties of the window object.
- JavaScript does not have classes; it only has object prototypes. It uses functions as classes.  You declare the properties inside the function and declare the methods by assigning them to the function object’s _prototype_.
- _prototype_ is an object shared by all instances of the object.  It forms part of a lookup chain, which has a special name called prototype chain.  Anything assigned to the object’s prototype becomes available to all instances of the object.
- Inner or nested functions can access variables in their parent function’s scope.
- Closure happens when an outer function returns the inner function and the inner function needs access to the outer function’s local variables.  The outer function’s scope object is actually retained even after the outer function has returned.  Only when there are no more references to the inner function will the outer function’s scope object be garbage collected.
- Scope objects form a chain called the scope chain.  Scope object is created every time the function starts executing.
