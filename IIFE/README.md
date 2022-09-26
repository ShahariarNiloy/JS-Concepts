# IIFE

#### According to MDN
> An IIFE (Immediately Invoked Function Expression) is a JavaScript function that runs as soon as it is defined.

**IIFE** - Immediately Invoked Function Expression, pronounced 'Iffy' by Ben Alman, who introduced the acronym.

#### Why?
When we define a function, the JavaScript engine adds the function to the global object.

```js
function add (a,b) {
    return a + b;
}
```
In web browsers, the JavaScript engine adds the add() function to the window global object:

```js
console.log(window.add);
```
Likewise, if we declare a variable outside of a function using the `var` keyword, the JavaScript engine also adds the variable to the global object:
```js
var counter = 10;
console.log(window.counter); // 10
```
If we have a lot of global variables and functions, the JavaScript engine will only free the memory that was allocated for them until the global object exits its scopes.

As a result, the script may consume Memory wastefully. Furthermore, having global variables and functions will most likely result in name clashes.

Using immediately invoked function expressions is one technique to prevent functions and variables from polluting the global object.

The following expression is called an immediately invoked function expression (IIFE) because the function is created as an expression and executed immediately:

```js
(function(a,b){
        return a + b;
})(10,20);
```

This is the general syntax for defining an IIFE:

```js
(function(){
    //...
})();

// or

(() => {
    //...
})();
```

By placing functions and variables inside an immediately invoked function expression, we can avoid polluting them to the global object:

```js
(function() {
    var counter = 0;

    function add(a, b) {
        return a + b;
    }

    console.log(add(10,20)); // 30
}());
```

##### Advantages of IIFE:

1. Do not create unnecessary global variables and functions
2. Functions and variables defined in IIFE do not conflict with other functions & variables even if they have same name.
3. Organize JavaScript code.
4. Make JavaScript code maintainable.

#### Questions

What will log to console the following code snippet:
```js
(function () {
  var first = second = 5;
})();

console.log(second);
```
##### Answer

```js
5
```
The answer would be 5 even though it seems as if the variable was declared within a function and can't be accessed outside of it. This is because
```js
var first = second = 5;
```
is interpreted the following way:
```js
var first = second;
second = 5;
```

But `second` is not declared anywhere in the function with `var` so it is set equal to 5 in the global scope.