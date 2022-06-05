---
title: "Quick refresher on JavaScript's objects, prototypes and inheritance"
date: "2017-10-17"
categories: 
  - "javascript"
---

![](/technical-blog/assets/images/jsbloglogo.png) Here is how we commonly code JavaScript's objects, prototypes and inheritance.  You can copy the JavaScript code below and quickly run it on any online JavaScript compiler/runner app on the Internet.  I use [JS Bin](https://jsbin.com/kilujodupi/edit?js,console)

.

\[code language="javascript" light="true"\]
// If we don't need to create/instantiate objects, then an object literal will do
console.log("\*\*\*\*\*Object Literal\*\*\*\*\*");
var EmployeeMe = {
  FullName: "Rodan Sotto",
  HireDate: "12/1/2015",
  Save: function(){
    console.log("Employee saved: " + this.FullName + ", " + this.HireDate.toString());
  }
}

EmployeeMe.Save(); // displays "Employee saved: Rodan Sotto, 12/1/2015"

console.log(EmployeeMe); // displays the object literal itself
console.log(Object.getPrototypeOf(EmployeeMe)); // displays the object literal's prototype which is Object

// Otherwise, we would use a constructor function to define the properties of the class
console.log("\*\*\*\*\*Constructor Function\*\*\*\*\*");
var Employee = function(fullName, hireDate){
  this.FullName = fullName;
  this.HireDate = hireDate;
}

// ... and on the constructor's prototype property to define the methods of the class
// We actually can define the methods inside the constructor but it's common practice
//  to define them on the prototype to get the maximum benefit of the prototypal inheritance
Employee.prototype.Save = function(){
    console.log("Employee saved: " + this.FullName + ", " + this.HireDate.toString());  
}

var e = new Employee("Rodan Sotto", "12/1/2015");
e.Save(); // displays "Employee saved: Rodan Sotto, 12/1/2015"

console.log(Employee); // displays the Employee constructor
console.log(Employee.prototype); // displays an object containing the Save() method
console.log(Employee.prototype.constructor); // displays the original constructor (e.g. the Employee constructor)
console.log(Object.getPrototypeOf(e)); // displays the Employee prototype
console.log(Object.getPrototypeOf(Object.getPrototypeOf(e))); // displays Object

// To inherit from Employee, the following is the common pattern used
// Notice the call to Employee.call(), this calls the Employee constructor but runs it in the context of the Manager by passing "this"
console.log("\*\*\*\*\*Inheritance\*\*\*\*\*");
var Manager = function(fullName, hireDate, companyShares){
  Employee.call(this, fullName, hireDate);
  this.CompanyShares = companyShares;
}

// The next statement is needed to allow Manager to inherit properties and methods defined on the Employee constructor's prototype
Manager.prototype = Object.create(Employee.prototype);

// Because of the previous statement, the Manager constructor's prototype's constructor is set to the Employee constructor
//  and we do not want that, so we need to fix this to point to the Manager constructor
Manager.prototype.constructor = Manager;

var m = new Manager("John Smith", "1/1/2000", 1000);
m.Save();
console.log(Manager); // displays the Manager constructor
console.log(Manager.prototype); // displays an object containing the constructor property and the inherited Save() method
console.log(Manager.prototype.constructor); // displays the Manager constructor
console.log(Object.getPrototypeOf(m)); // displays the Manager prototype
console.log(Object.getPrototypeOf(Object.getPrototypeOf(m))); // displays Employee prototype
console.log(Object.getPrototypeOf(Object.getPrototypeOf(Object.getPrototypeOf(m)))); // displays Object

// As we can see in the last three statements how Manager inherits Employee
//  and the Employee inherits from Object by traversing the prototype chain
\[/code\]
