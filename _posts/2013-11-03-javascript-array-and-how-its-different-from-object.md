---
title: "JavaScript Array and How It’s Different from Object"
date: "2013-11-03"
categories: 
  - "javascript"
---

It’s important to know arrays and objects in JavaScript because they are often used to store client-side data.  Below are quick points on arrays and objects:

// arrays and objects can be confusing at first  
// just remember that arrays in Javascript are ordered lists  
//  and are normally looped through using numerical index starting with 0  
// objects, on the other hand, have property names associated with values  
// confusion always happen when objects are used like associative arrays,  
//  arrays that use names as index to access their associated values  
      
      
// declaring an array  
      
// as an empty array  
var myArray1 = \[\];  
alert(myArray1.length); // displays 0, since it"s empty  
      
// with initialized values  
var myArray2 = \["apple", "orange", "banana", "strawberry"\];  
alert(myArray2\[1\]); // displays orange, the second element in the array  
      
// using Array constructor  
var myArray3 = new Array("red", "green", "blue");  
alert(myArray3.join(", ")); // displays red, green, blue  
      
      
// object on the other hand has a different declaration syntax  
// while array is declared using square brackets \[\],  
//  object is declared using curly braces {}  
// BUT both use \[\] to access their elements/properties  
var myObject1 = {};  
var myObject2 = {  
    "fruit1": "apple",  
    "fruit2": "orange",  
    "fruit3": "banana",  
    "fruit4": "strawberry"  
}  
alert(myObject2\["fruit2"\]); // displays orange  
      
      
// one method that is quite used most often for arrays is the push() method  
// it"s a convenient way to add to your array  
alert(myArray2.length); // displays 4  
myArray2.push("grape");  
myArray2.push("cherry");  
alert(myArray2.length); // displays 6, after adding 2 more in the array  
  

  

Hopefully that helps clarify the confusion.

[JavaScript Kit](http://www.javascriptkit.com/jsref/) has a comprehensive reference with explanations and examples including reference to Array object that you might want to look further into; definitely a good resource to add to your toolbox.  I already had it added to my Favorite Links.

Also, [Fun with JavaScript Native Array Functions](http://flippinawesome.org/2013/11/25/fun-with-javascript-native-array-functions/) talks about a slew of array functions in detail.
