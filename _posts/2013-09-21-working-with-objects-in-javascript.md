---
title: "Object Oriented Programming In Javascript"
date: "2013-09-21"
categories: 
  - "javascript"
---

Yes, there is OOP in JavaScript.  The below code are notes that I took during my first week of Advanced Javascript class that I am currently enrolled in at Ryerson University.  These are working code.  I used the free [Komodo](http://komodoide.com/komodo-edit/) editor from ActiveState.  It is a cool editor with colored syntax and intellisense and works with HTML and Javascript, and even Perl, PHP, Phyton and Ruby.

// creating native object types like dates, strings, numbers, and booleans  
var date = new Date();  
var str1 = "Sotto";  
var str2 = new String("Rodan");  
var num1 = 0.35;  
var num2 = new Number(0.4);  
var bool1 = true;  
var bool2 = new Boolean(false);  
      
// calling native object types' properties and methods  
var strLen = str1.length;  
var fixedNum = num1.toFixed(4);  
      
// creating custom objects, in this example blank objects  
var obj1 = new Object();  
var obj2 = {};  
      
// adding properties and methods after creating a custom object  
obj1.prop1 = "Object1's Property1";  
obj1\["prop1"\] = "Object1's Property1 using \[\]";  
obj1.func1 = function () {  
    return "Object1's Function1";  
};  
obj1\["func1"\] = function () {  
    return "Object1's Function1 using \[\]";  
};  
      
// you can also add properties and methods to the native objects  
//  using the prototype object  
Date.prototype.myCustomProperty = "My Custom Property";  
var date = new Date();  
//alert(date.myCustomProperty);  
      
// some like the Math object does not have the prototype object  
//  so you add directly  
Math.myCustomProperty = "My Custom Property";  
//alert(Math.myCustomProperty);  
      
// removing property or function from an object  
delete obj1.func1;  
obj1.func1(); // displays undefined  
      
// creating a custom object with properties and functions  
// notice you use , to separate each properties and functions in {}  
var invoice = {  
  taxRate: 0.35,  
  dueDays: 30,  
  getSalesTax: function(subTotal) {  
    return (subTotal \* invoice.taxRate);  
  },  
  getTotal: function(subTotal, salesTax) {  
    return (subTotal + salesTax);  
  }  
};  
      
// creating object references  
var today2 = new Date();  
var now = today2;  
      
// creating a class  
// you create a constructor function first  
var Vehicle = function(make, model) {  
    this.make = make;  
    this.model = model;  
    this.miles = 0;  
}  
      
// then create the class methods and other properties  
//  through the prototype object  
Vehicle.prototype.drive = function(miles) {  
    this.miles += miles;  
    return this;  
}  
      
Vehicle.prototype.canFly = false;  
      
var myCar = new Vehicle("Honda", "CRV");  
myCar.drive(300);  
      
// creating a sub class (inheritance)  
var Car = function(make, model, door, suv) {  
    this.make = make;  
    this.model = model;  
    this.door = door;  
    // example of optional arguments  
    if (arguments.length == 4) {  
        this.suv = suv  
    }  
    else {  
        this.suv = false;  
    };  
    this.miles = 0;  
};  
      
Car.prototype = new Vehicle();  
      
var my2ndCar = new Car("Honda", "Odyssey", 4, false);  
my2ndCar.drive(50).drive(100);  
      
// notice above the method is called one after the other  
// this is possible if the method is a cascading method  
// a cascading method is one that returns the this object  
      
// looping through the object's properties and methods  
for (var property in my2ndCar) {  
    alert(property);  
}  
      
// checking if the object's property is enumerable  
alert(my2ndCar.propertyIsEnumerable("make")); // displays true  
alert(my2ndCar.propertyIsEnumerable("drive")); // displays false  
      
// using the in operator  
alert("make" in my2ndCar); // displays true  
alert("drive" in my2ndCar); // displays true  
      
// using the instanceof operator  
alert(my2ndCar instanceof Car); // displays true  
alert(my2ndCar instanceof Vehicle); // displays true  
alert(my2ndCar instanceof Object); // displays true  
alert(my2ndCar instanceof String); // displays false  
      
// using the typeof operator  
alert(typeof my2ndCar); // displays object  
alert(typeof Vehicle); // displays function  
alert(typeof Car); // displays function  
alert(typeof my2ndCar.make); // displays string  
alert(typeof my2ndCar.drive); // displays function
