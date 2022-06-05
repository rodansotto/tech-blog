---
title: "TypeScript Notes: Part 2"
date: "2017-10-16"
categories: 
  - "javascript"
---

![](/technical-blog/assets/images/tslogo.png) Part 2 is all about classes, interfaces, abstract classes, and inheritance in TypeScript.  It's similar to OOP in C#.  So easy to grasp and use that one might totally forget how OOP in JavaScript works.  Same as in [TypeScript Notes: Part 1](https://rodansotto.wordpress.com/2017/09/08/typescript-notes-part-1/), I will present the TypeScript code and the generated JavaScript code.  The generated JavaScript code might be overwhelming to understand at first but as long as your knowledge with JavaScript objects is still intact, you should be able to figure it out.  For a refresher, read [MDN's Introducing JavaScript objects](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects)

.

\[code language="javascript"\]
// TypeScript Notes: Part 2

// Classes, access modifiers, properties, constructor
class Employee {
    FullName: string;
    public HireDate: Date; // this is a Javascript Date object
    private Salary: number;
    protected HomeAddress: string;

    // properties / accessors
    private \_position: string;
    get Position(): string {
        return this.\_position;
    }
    set Position(position: string) {
        this.\_position = position;
    }

    // constructor
    constructor() {
        console.log("Employee object created");
    }

    Save(): void {
        console.log("Employee saved: " + this.FullName + ", " + this.HireDate.toLocaleDateString());
    }
}

let e: Employee = new Employee(); // displays "Employee object created"
e.FullName = "Rodan Sotto";
e.HireDate = new Date("12/1/2015");
e.Save(); // displays "Employee saved: Rodan Sotto, 12/1/2015"

e.Salary = 0; // compile-time error because e.Salary is declared private; default access modifier is public
console.log("Salary set to " + e.Salary);

e.HomeAddress = "Mississauga, ON"; // compile-time error because e.HomeAddress is protected
console.log("Home address set to " + e.HomeAddress);

e.Position = "Senior Software Developer";
console.log("Position set to " + e.Position); // displays "Position set to Senior Software Developer"
// Note: To support properties / accessors, at minimum, ES5 is required

// Using shorthand properties to initialize properties at construction
class Employer {
    // specifying access modifier before constructor parameter makes it a property
    // in the example below, Name and Address are properties while misc is not
    constructor(public Name: string, public Address: string, misc: string) {
    }
}

let er: Employer = new Employer("Acme Company", "Ontario, Canada", "xyz");
console.log("Employer: " + er.Name + ", " + er.Address); // displays "Employer: Acme Company, Ontario, Canada"

// Inheritance, protected variables in derived classes
class Manager extends Employee {
    constructor(public CompanyShares: number, address: string) {
        super(); // required call for derived classes
        this.HomeAddress = address; // protected variable is accessible to derived classes
    }

    // method to return the protected variable HomeAddress
    GetHomeAddress(): string {
        return this.HomeAddress;
    }
}

let m: Manager = new Manager(1000, "Toronto, ON"); // displays "Employee object created"
m.FullName = "John Smith";
m.HireDate = new Date("1/1/2000");
m.Position = "Development Manager";
m.Save(); // displays "Employee saved: John Smith, 1/1/2000"
console.log("Company shares set to " + m.CompanyShares); // displays "Company shares set to 1000"
console.log("Home address set to " + m.GetHomeAddress()); // displays "Home address set to Toronto, ON"

// Template strings
// To use, enclose your template string with the tick symbol (\`)
//  and enclose the variables in ${} notation
console.log(\`Manager ${m.FullName} is hired ${m.HireDate.toLocaleDateString()} as a ${m.Position} and he lives in ${m.GetHomeAddress()}\`);
// displays "Manager John Smith is hired ?1?/?1?/?2000 as a Development Manager and he lives in Toronto, ON"

// Interfaces
interface ICanSing {
    Sing(): void;
}

interface ICanDance {
    Dance(): void;
}

class Person implements ICanSing, ICanDance {
    constructor(public Name: string) {
    }

    Sing(): void {
        console.log(\`${this.Name} can sing!\`);
    }

    Dance(): void {
        console.log(\`${this.Name} can dance!\`);
    }
}

let j: Person = new Person("Jane");
j.Sing(); // displays "Jane can sing!"
j.Dance(); // displays "Jane can dance!"

// Abstract classes
// In an abstract class you can have partial implementation while in an interface you cannot
// Plus you cannot extend more than one abstract class while you can implement more than one interface
abstract class AbstractPerson {
    ShowAbilities(): void {
        if (this.CanSing) this.Sing();
        if (this.CanDance) this.Dance();
    }

    CanSing: boolean;
    CanDance: boolean;
    abstract Sing(): void;
    abstract Dance(): void;
}

class AnotherPerson extends AbstractPerson {
    constructor(public Name: string) {
        super();
    }

    Sing(): void {
        console.log(\`${this.Name} can sing!\`);
    }

    Dance(): void {
        console.log(\`${this.Name} can dance!\`);
    }
}

let k = new AnotherPerson("Kane");
k.CanSing = true;
k.CanDance = false;
k.ShowAbilities();
\[/code\]

  

\[code language="javascript"\]
// Generated JavaScript Code From TypeScript Notes: Part 2

// Classes, access modifiers, properties, constructor
var Employee = /\*\* @class \*/ (function () {
    // constructor
    function Employee() {
        console.log("Employee object created");
    }
    
	Object.defineProperty(Employee.prototype, "Position", {
        get: function () {
            return this.\_position;
        },
        set: function (position) {
            this.\_position = position;
        },
        enumerable: true,
        configurable: true
    });
    
	Employee.prototype.Save = function () {
        console.log("Employee saved: " + this.FullName + ", " + this.HireDate.toLocaleDateString());
    };
    
	return Employee;
}());

var e = new Employee(); // displays "Employee object created"
e.FullName = "Rodan Sotto";
e.HireDate = new Date("12/1/2015");
e.Save(); // displays "Employee saved: Rodan Sotto, 12/1/2015"

e.Salary = 0;
console.log("Salary set to " + e.Salary);

e.HomeAddress = "Mississauga, ON";
console.log("Home address set to " + e.HomeAddress);

e.Position = "Senior Software Developer";
console.log("Position set to " + e.Position); // displays "Position set to Senior Software Developer"

// Using shorthand properties to initialize properties at construction
var Employer = /\*\* @class \*/ (function () {
    function Employer(Name, Address, misc) {
        this.Name = Name;
        this.Address = Address;
    }
    
	return Employer;
}());

var er = new Employer("Acme Company", "Ontario, Canada", "xyz");
console.log("Employer: " + er.Name + ", " + er.Address); // displays "Employer: Acme Company, Ontario, Canada"

// Inheritance, protected variables in derived classes
var Manager = /\*\* @class \*/ (function (\_super) {
    \_\_extends(Manager, \_super);
    
	function Manager(CompanyShares, address) {
        var \_this = \_super.call(this) || this;
        \_this.CompanyShares = CompanyShares;
        \_this.HomeAddress = address;
        return \_this;
    }
    
    Manager.prototype.GetHomeAddress = function () {
        return this.HomeAddress;
    };
    
	return Manager;
}(Employee));

var m = new Manager(1000, "Toronto, ON"); // displays "Employee object created"
m.FullName = "John Smith";
m.HireDate = new Date("1/1/2000");
m.Position = "Development Manager";
m.Save(); // displays "Employee saved: John Smith, 1/1/2000"
console.log("Company shares set to " + m.CompanyShares); // displays "Company shares set to 1000"
console.log("Home address set to " + m.GetHomeAddress()); // displays "Home address set to Toronto, ON"

// Template strings

console.log("Manager " + m.FullName + " is hired " + m.HireDate.toLocaleDateString() + " as a " + m.Position + " and he lives in " + m.GetHomeAddress());

// Interfaces

var Person = /\*\* @class \*/ (function () {
    function Person(Name) {
        this.Name = Name;
    }
    
	Person.prototype.Sing = function () {
        console.log(this.Name + " can sing!");
    };
    
	Person.prototype.Dance = function () {
        console.log(this.Name + " can dance!");
    };
    
	return Person;
}());

var j = new Person("Jane");
j.Sing(); // displays "Jane can sing!"
j.Dance(); // displays "Jane can dance!"

// Abstract classes

var AbstractPerson = /\*\* @class \*/ (function () {
    function AbstractPerson() {
    }

    AbstractPerson.prototype.ShowAbilities = function () {
        if (this.CanSing)
            this.Sing();
        if (this.CanDance)
            this.Dance();
    };

    return AbstractPerson;
}());

var AnotherPerson = /\*\* @class \*/ (function (\_super) {
    \_\_extends(AnotherPerson, \_super);
    
	function AnotherPerson(Name) {
        var \_this = \_super.call(this) || this;
        \_this.Name = Name;
        return \_this;
    }
    
	AnotherPerson.prototype.Sing = function () {
        console.log(this.Name + " can sing!");
    };
    
	AnotherPerson.prototype.Dance = function () {
        console.log(this.Name + " can dance!");
    };
    
	return AnotherPerson;
}(AbstractPerson));

var k = new AnotherPerson("Kane");
k.CanSing = true;
k.CanDance = false;
k.ShowAbilities();

// This is the \_\_extends code used to implement classes extending another class or abstract class in Typescript
var \_\_extends = (this && this.\_\_extends) || (function () {
    var extendStatics = Object.setPrototypeOf ||
        ({ \_\_proto\_\_: \[\] } instanceof Array && function (d, b) { d.\_\_proto\_\_ = b; }) ||
        function (d, b) { for (var p in b) if (b.hasOwnProperty(p)) d\[p\] = b\[p\]; };
    
	return function (d, b) {
        extendStatics(d, b);
        function \_\_() { this.constructor = d; }
        d.prototype = b === null ? Object.create(b) : (\_\_.prototype = b.prototype, new \_\_());
    };
})();
\[/code\]
