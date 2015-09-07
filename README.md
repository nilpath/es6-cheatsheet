# EcmaScript 6 Cheat Sheet

**This document is currently a work in progress. any feedback or pull requests are appreciated.**

## Purpose
The main purpose of this document is to give an overview of the new features in EcmaScript 6 as well as to act as a quick reference for syntax look-up.

## Table of Contents

* [Purpose](#purpose)
* [Table of Contents](#table-of-contents)
* [let & const](#let--const)
 * [let](#let)
 * [const](#const)
* [Destructuring](#destructuring)
 * [Array Destructuring](#array-destructuring)
 * [Object Destructuring](#object-destructuring)

## let & const

There are two new ways to declare variables in EcmaScript 6, ```let``` and ```const```. However, they work a bit differently than ```var```.

### let
```javascript

/*
 Produces a ReferenceError when variable is used before declared.
*/

console.log(x); // => ReferenceError.
let x;

/*
 Produces a SyntaxError when declaring a variable more than once.
*/

let x = 'foo';
...
let x = 'bar'; // => SyntaxError.

/* 
 They are scoped to a code block rather than a function block.
*/

function foo() { // function scope
  
  if(...) { // code block
    let foo = 'foo';
    var bar = 'bar'; 
  }
  
  console.log(foo); // => ReferenceError.
  console.log(bar); // => 'bar'
  
}

/*
 variables declared globally with let are not attached to the global object. 
 Instead they are attached to the global block.
*/

let foo = 'foo';
var bar = 'bar';

console.log(window.foo); // => undefined.
console.log(window.bar); // => 'bar'.

/*
 a let variable defined in a loop is regarded as a fresh variable for each iteration.
*/

let arr = ['one', 'two', 'three'];

for (var x = 0; x < arr.length; x++) {
  setTimeout(function(){
    console.log(arr[x]);
  }, x * 3000)
}

// => outputs arr[3], undefined, 3 times.

for (let x = 0; x < arr.length; x++) {
  setTimeout(function(){
    console.log(arr[x]);
  }, x * 3000)
}

// => outputs arr[0], arr[1] and arr[2].

```

### const
Declaring constants, using ```const```, works mostly the same as ```let``` but with a few differences.

```javascript
/* 
 A constant can only be assigned a value once.
*/

const MY_CONST = 'constant';
...
const MY_CONST = 'new constant'; // => SyntaxError.

/*
 Declaring a const without a value will create an error.
*/

const MY_CONST; // => SyntaxError.

```

## Destructuring
Destructuring is the new way for assigning the properties of an Array or Object in a more readable way

### Array Destructuring
```javascript
/*
  Arrays and other iterables are destructured using brackets.
*/

[one, two, three] = [1, 2, 3];
console.log(one, two, three); // => 1 2 3

/*
 You can declare the destructured variables 
 by putting var, let or const before the assignment.
*/

let [one, two, three] = [1, 2, 3];

/*
 Properties can be skipped using commas.
*/

var [,,, four] = [1, 2, 3, 4];
console.log(four); // => 4.

/* 
  You can create a trailing array using the rest operator.
*/

var [item, ...otherItems] = ['all', 'my', 'other', 'items'];
console.log(otherItems); // => ['my', 'other', 'items'].

/*
 Even nested Arrays can be destructured
*/

var [one, [[two], [three]], four] = [1, [[2], [3]], 4];
console.log(one, two, three, four); // => 1 2 3 4.

/*
 Properties out of bounds are undefined.
*/

var [isUndefined] = [];
console.log(isUndefined); // => undefined.

/*
 default values can be defined for missing values.
*/

var [isUndefined = true] = [];
console.log(isUndefined); // => true.

```
### Object Destructuring
```javascript
/*
  Objects uses curly brackets for destructuring.
*/

var {name, age} = {name: 'Smith', age: 40};
console.log(name, age); // => Smith 40.

/*
 Variables need to be declared when destructuring Objects.
*/

{ name } = {name: 'Smith'}; // => SyntaxError.
({ name } = {name: 'Smith'}); // => is OK.

/* 
 Properties can be renamed with the following syntax {property : new_name}
*/

var {name: agent} = {name: 'Smith'};
console.log(agent); // => Smith.

/*
 Object and Arrays can be destructured in combination.
*/

var nestedObjectWithArray = {
  first: 1,
  array: [2, {third: 3}, 4]
};

var {first, [second, {third} , fourth]} = nestedObjectWithArray;
console.log(first, second, third, fourth); // => 1 2 3 4.

/*
 Missing properties are undefined.
*/

var {name} = {};
console.log(name); // => undefined.

/*
 default values can be defined for missing values.
*/

var {name = 'Andersson'} = {};
console.log(name); // => Andersson.
```
