# Hoisting

#### According to MDN
> JavaScript Hoisting refers to the process whereby the interpreter appears to move the declaration of functions, variables or classes to the top of their scope, prior to execution of the code.

#### According to W3Schools
> Hoisting is JavaScript's default behavior of moving declarations to the top.

When the JavaScript engine executes the JavaScript code, it creates the *global execution context*. The *global execution context* has two phases:

*   Creation
*   Execution

During the creation phase, the JavaScript engine moves the variable and function declarations to the top of the code. Not physically, but in memory. This is known as **Hoisting** in JavaScript.

### Variable Hoisting

We usually write code like this:
```js
var x = 10;
```
Here, actually two things is happening. One, declaration and another one is assigning a value.
```js
var x; // declaration of the variable
x = 10; // assigning a value to that variable
```
Javascript code parse in the down direction. That means, code first execute what is written in the first line, then second line, then third line and by so, way down to the bottom.

```js
var x;
x = 10;
console.log(x) // 10
```
This is the common behavior of any code. First declaring the variable, then assigning a value `10` to it. And after that, when we log the value and we're getting it.
One thing to notify here, in javascript when we declare any variable, by default javascript assign `undefined` to it, before assigning any actual value. So if we do the following,
```js
var x;
console.log(x); // undefined
```
Which is also act fine. We declare a variable, then javascript assign `undefined` to it. So when we log the value, we are getting `undefined`.
<br>
But interesting things happen, if we do the following:

```js
console.log(x); // undefined
var x;
```

From the normal code behavior, we should get an error that we are accessing a variable before defining it. But rather we are getting `undefined` printed.
This is where we can see the glimpse of **Hoisting**. From the definition, we know javascript move all the declaration to the top of the script or more precisely, to the top of the accessible scope. So here, we are accessing the variable `x` before declaring but under the hood javascript move the declaration to the top and assign `undefined` to it. That is why we did not see any error.

**Hoisting** behave differently with `var` and `(let / const)`

**Hoisting** with `var` keyword: The actual concept of **Hoisting** can be seen with the `var` keyword.
```js
console.log(x); // undefined
var x = 10;
```
In this example, we reference the `x` variable before the declaration.

However, the first line of code doesn’t cause an error. The reason is that the JavaScript engine moves the variable declaration to the top of the script.

Technically, the code looks like the following in the execution phase:
```js
var x;

console.log(x); // undefined
x = 10;
```

**Hoisting** with `let/const` keyword: Javascript does hoist variable with the `let` or `const` keyword. Means, the variable move up to its accessible scope but does not initialize `undefined`. That is why we encounter with `Reference Error`.

The following declares the variable `x` with the let keyword:
```js
console.log(x);
let x = 10;
```

The JavaScript issues the following error:
```bash
ReferenceError: Cannot access 'x' before initialization
```

The error message explains that the `x` variable is already in the heap memory. However, it hasn’t been initialized.

Behind the scenes, the JavaScript engine hoists the variable declarations that use the `let` keyword. However, it doesn’t initialize the `let` variables.

Notice that if we access a variable that doesn’t exist, the JavaScript will throw a different error:
```js
console.log(x);
let y = 10;
```
Here is the error:
```bash
ReferenceError: 'x' is not defined
```

`let` keyword variable does hoist but javascript only define that variable but does not initialize with anything like `undefined`.

### Function Hoisting

JavaScript functions can be loosely classified as the following:

1. Function declarations
2. Function expressions

##### Function Declarations 
Function declarations are when we create a function and give it a name. We declare the name of the function when we write the `function` keyword, followed by the function name. For example:
```js
function myFunction() {
  // ---
};
```
Like variables, the JavaScript engine also **Hoists** the function declarations. This means that the JavaScript engine also moves the function declarations to the top of the script. For example:
```js
console.log(add(10, 20)); // 30

function add(a, b) {
  return a + b;
}
```
In this example, we called the add() function before defining it. The above code is equivalent to the following:
```js
function add(a, b){
    return a + b;
}

console.log(add(10, 20)); // 30
```
During the creation phase of the execution context, the JavaScript engine places the `add()` function declaration in the heap memory. To be precise, the JavaScript engine creates an object of the `Function` type and a function reference called add that refers to the function object.

##### Function expressions

Function expressions are when we create a function and assign it to a variable. The function is usually anonymous, which means it doesn’t have a name. For example:
```js
let myFunction = function() {
  // ---
};

myFunction();
```
As we can see, the function is assigned to the `myFunction` variable. This means that we must define the function before you can call it. And now we can call this function by this `myFunction` variable.
But Function expressions are not **hoisted**, so we can’t use them before they are defined in our code.
The following code won't work.
```js
x();

let x = function() {
  console.log('Anything');
};
```
If we execute the code, the following error will occur:
```bash
TypeError: 'x' is not a function
```

Similar to the functions expressions, arrow functions are not hoisted.

##### Question 
What will be the output of the following code snippet:
```js
function Add(){
    console.log(answer);
    var answer = 2;
};
Add()
```
##### Answer
```bash
undefined
```
What will be the output of the following code snippet: 
```js
display();
var temp= 'hi';
function display(){
    console.log(temp);
    var temp = 'bye';
};
```

##### Answer
```bash
undefined
```