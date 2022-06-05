---
title: "TypeScript Notes: Part 1"
date: "2017-09-08"
categories: 
  - "javascript"
---

![]({{ site.baseurl }}/assets/images/tslogo.png) I decided to post a series of notes on TypeScript and this is Part 1.  I think understanding what TypeScript does makes you a better JavaScript programmer as you will come to know the issues inherent in JavaScript.  The format I will be using is to present the TypeScript code and explain it along the way in the comments itself and then present the generated JavaScript code.  You can play with the code by copying it and pasting it on any online TypeScript compiler/runner app.  I recommend [Playground TypeScript](https://www.typescriptlang.org/play/)

.  So let's get to it and no more dilly dally.

```ts
// TypeScript Notes: Part 1

// Using var
// Works almost the same way as using var in Javascript
var myDeclaredVar = "Rodan Sotto";
console.log(myDeclaredVar); // displays "Rodan Sotto"
//console.log(myUndeclaredVar); // compile-time error; in JavaScript it's a runtime error
console.log(myHoistedVar); // displays "undefined"; no error because all JavaScript var declarations anywhere in the code are moved up and made available from line 1 (concept called hoisting)
var myHoistedVar = 5;

var myNoBlockLevelScopingVar = 5;
if (myNoBlockLevelScopingVar > 2) {
    var myNoBlockLevelScopingVar = 6;
    console.log(myNoBlockLevelScopingVar); // displays 6 as expected
}
console.log(myNoBlockLevelScopingVar); // displays 6 as well because JavaScript var declarations don't have block level scoping

// Using let
// This solves issues with variable hoisting and no block level scoping
let myLetVar = "Rodan Sotto";
console.log(myLetVar);
console.log(myNotHoistedLetVar); // compile-time error because let does not allow hoisting variables
let myNotHoistedLetVar;

let myBlockLevelScopingLetVar = 5;
if (myBlockLevelScopingLetVar > 2) {
    let myBlockLevelScopingLetVar = 6;
    console.log(myBlockLevelScopingLetVar); // displays 6 as expected
}
console.log(myBlockLevelScopingLetVar) // displays 5 because let allows block level scoping (check the generated JavaScript code how it does this)

// Using const
const myConst = 5;
myConst = 6; // compile-time error because const does not allow changing the values of constant or read-only variables

// Data types: number, string, and boolean
let n: number = 123;
let s: string = "ABC";
let b: boolean = true;
n = "DEF"; // compile-time error because TypeScript is type safe
s = 456; // compile-time error
b = "GHI"; // compile-time error

let myTypeInferedVar = 1;
myTypeInferedVar = "A"; // compile-time error because TypeScript has type inference that decides the type of datatype-less variables based on first assignment

let myNotTypeInferedVar; // notice that there is no initialization here
myNotTypeInferedVar = 1;
console.log(myNotTypeInferedVar); // displays 1
myNotTypeInferedVar = "A";
console.log(myNotTypeInferedVar); // displays "A"; no compile-time error because varialbles with no data type specified is by default has an implicit datatype of any

// Data type any
// This is default datatype for datatype-less variables
// Use it when it is a must because it is not a best practice always.
let myAnyTypeVar: any;
myAnyTypeVar = 1;
console.log(myAnyTypeVar); // displays 1
myAnyTypeVar = "A";
console.log(myAnyTypeVar); // displays "A"

// Generic arrays
// Just like the C# generic collection
let myNumberArray: Array<number> = new Array<number>();
myNumberArray.push(1);
myNumberArray.push(2);
myNumberArray.push("c-sharp"); // compile-time error

// Functions in TypeScript ...
// ... forces you to return
function myNumberFunction(): number {
    return 1; // without this return statement will produce compile-time error
}

// but following function declarations will not force you to return
function myVoidFunction(): void { } // you cannot have return statement here
// or
function myAnyFunction(): any { } // you can have return statement here
// or
function myFunction() { } // by default the return type is any

// ... has parameter checking
function myFunctionWithParams(x: number, y: number): void {
    console.log(x + y);
}
myFunctionWithParams(1, 2);
myFunctionWithParams(1, 2, 3); // compile-time error

// ... does not allow duplicate function names regardless if parameters are different
function myDuplicateFunction(x: number, y: number): void { }
function myDuplicateFunction(x: number, s: string, b: boolean): void { } // compile-time error

// ... has optional parameters
function myFunctionWithOptionalParams(x: number, y?: number): void {
    console.log(x);
    console.log(y);
}
myFunctionWithOptionalParams(1, 2); // displays 1 and 2
myFunctionWithOptionalParams(1); // displays 1 and "undefined"

// ... hs rest parameter which allows defining function with array as parameters
function myFunctionWithRestParam(...x: Array<number>): void {
    for (let e of x) {
        console.log(e);
    }
}

myFunctionWithRestParam(1, 2); // displays 1 and 2
myFunctionWithRestParam(3, 4, 5); // displays 3, 4, and 5
myFunctionWithRestParam(6, 7, 8, 9, 0); // displays 6, 7, 8, 9, and 0
```

  

```js
// Generated JavaScript Code From TypeScript Notes: Part 1

var myDeclaredVar = "Rodan Sotto";
console.log(myDeclaredVar); // displays "Rodan Sotto"
//console.log(myUndeclaredVar); // runtime error
console.log(myHoistedVar); // displays "undefined"
var myHoistedVar = 5;

var myNoBlockLevelScopingVar = 5;
if (myNoBlockLevelScopingVar > 2) {
    var myNoBlockLevelScopingVar = 6;
    console.log(myNoBlockLevelScopingVar); // displays 6 as expected
}
console.log(myNoBlockLevelScopingVar); // displays 6 as well

var myLetVar = "Rodan Sotto";
console.log(myLetVar);
console.log(myNotHoistedLetVar);
var myNotHoistedLetVar;

var myBlockLevelScopingLetVar = 5;
if (myBlockLevelScopingLetVar > 2) {
    var myBlockLevelScopingLetVar\_1 = 6;
    console.log(myBlockLevelScopingLetVar\_1); // displays 6 as expected
}
console.log(myBlockLevelScopingLetVar); // displays 5

var myConst = 5;
myConst = 6;

// Data types: number, string, and boolean
var n = 123;
var s = "ABC";
var b = true;
n = "DEF";
s = 456;
b = "GHI";

var myTypeInferedVar = 1;
myTypeInferedVar = "A";

var myNotTypeInferedVar;
myNotTypeInferedVar = 1;
console.log(myNotTypeInferedVar); // displays 1
myNotTypeInferedVar = "A";
console.log(myNotTypeInferedVar); // displays "A"

var myAnyTypeVar;
myAnyTypeVar = 1;
console.log(myAnyTypeVar); // displays 1
myAnyTypeVar = "A";
console.log(myAnyTypeVar); // displays "A"

var myNumberArray = new Array();
myNumberArray.push(1);
myNumberArray.push(2);
myNumberArray.push("c-sharp");

function myNumberFunction() {
    return 1;
}

function myVoidFunction() { }

function myAnyFunction() { }

function myFunction() { }

function myFunctionWithParams(x, y) {
    console.log(x + y);
}
myFunctionWithParams(1, 2);
myFunctionWithParams(1, 2, 3);

function myDuplicateFunction(x, y) { }
function myDuplicateFunction(x, s, b) { }

function myFunctionWithOptionalParams(x, y) {
    console.log(x);
    console.log(y);
}
myFunctionWithOptionalParams(1, 2); // displays 1 and 2
myFunctionWithOptionalParams(1); // displays 1 and "undefined"

function myFunctionWithRestParam() {
    var x = \[\];
    for (var \_i = 0; \_i < arguments.length; \_i++) {
        x\[\_i - 0\] = arguments\[\_i\];
    }
    for (var \_a = 0, x\_1 = x; \_a < x\_1.length; \_a++) {
        var e = x\_1\[\_a\];
        console.log(e);
    }
}
myFunctionWithRestParam(1, 2); // displays 1 and 2
myFunctionWithRestParam(3, 4, 5); // displays 3, 4, and 5
myFunctionWithRestParam(6, 7, 8, 9, 0); // displays 6, 7, 8, 9, and 0
```
