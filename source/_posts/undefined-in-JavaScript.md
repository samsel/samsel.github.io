title: undefined in JavaScript
date: 2013-07-11 20:13:22
tags: ["javascript"]
---

JavaScript is very flexible that sometimes not knowing to use it safely
would end up causing pitfalls. This post explains the traps of _undefined_
in JavaScript and ways to overcome them.

_undefined_ is one of JavaScript's six primitive data types.

``` javascript data types
string, number, boolean, null, undefined, object
```

_undefined_ is implemented in Javascript as a property of the global object with value _undefined_. It is the the default value for all initialized variables with no assignment and functions without any return value.

``` javascript type test
//example 1
typeof undefined // "undefined"
//
//example 2
var a;
typeof a // "undefined"
//
//example 3
function sample() {}
sample() // returns undefined
//
//example 4
var b = {};
b.test // returns undefined
```

The interesting thing about _undefined_ is that it is mutable in versions of JavaScript below EcmaScript 5. The language allows different values of different data types to be set on _undefined_ which might cause some worse programming behaviours. Some examples of assigning values to _undefined_ are as below.

``` javascript assign values to undefined
//example 1
var undefined = "s";
//
//example 2
(function(undefined) { 
  typeof undefined; // "string"
}("1")); 
//
//example 3
(function(undefined) { 
  typeof undefined; // "number"
}(1)); 
```

One of the most prominant ways to avoid the above effect of assigning unwanted values to undefined and to make sure that undefined has it default intented value is to use the below pattern. It could be seen in jQuery source and a lot of plugins as well.

``` javascript undefined reset
(function(undefined, undefined) { 
	typeof undefined; // "undefined"
}("1")); 
```

Another way to make sure that _undefined_ is set properly is to use the uncommon JavaScript language feature _void_. It is a function which when used with an expression, executes the expression and returns _undefined_.

``` javascript undefined reset
//example 1
var a = void (2+3);
typeof a // "undefined"

//example 2
void(0); // returns undefined
```

But the best of all elegant solution would be to use strict mode. [Strict mode](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode"Strict mode") in EcmaScript 5 changes all silently failing errors into throwable errors in JavaScript.


``` javascript 'use strict'
function foo() {
	undefined = 123;
}
//
function bar() {
	'use strict';
	undefined = 123;
}
//
// foo function can be executed without any errors
foo();
//
// but, executing bar, throws error because of the strict mode.
bar();
TypeError: Cannot assign to read only property 'undefined' of [object Object]
```
