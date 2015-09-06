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

## let & const

```let``` and ```const``` are new ways to declare variables, just like ```var```. However, they work a bit differently.

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
```const``` works mostly the same as ```let``` with a few differences.

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



