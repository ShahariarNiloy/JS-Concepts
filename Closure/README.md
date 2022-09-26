# Closure
#### According to MDN
> A closure is the combination of a function bundled together (enclosed) with references to its surrounding state (the lexical environment). In other words, a closure gives you access to an outer function's scope from an inner function. In JavaScript, closures are created every time a function is created, at function creation time.

#### According to W3Schools
> A closure is a function having access to the parent scope, even after the parent function has closed.

A **Closure** is a programming technique that allows variables to be accessed outside of the scope of a function. A closure is typically created when a function is defined within another function, allowing the inner function to access variables in the outer function even after the outer function has been executed.


<span style="color:red"><i>**NOTE: Closure is often confused with Lexical Scope. Lexical Scope is an important part of closure, but it is not closure by itself.</i></span>

#### Lexical Scope

Lexical scope is the ability for a function scope to access variables from the parent scope.

##### Example:
```js
// global scope
let x = 1;

const outerFunc = () => {
    // local scope
    let y = 2;

    console.log(x); 
    console.log(y); 

    const innerFunc = () => {
        console.log(x += 5) 
        console.log(y += 2) 
    }

    innerFunc();
}

outerFunc();
```
##### Output
```js
1 // x
2 // y
6 // updated x by innerFunc
4 // updated y by innerFunc
```
It is an important part of closure, but it is not closure by itself.

##### Re-writing the code for ***Closure Example***
```js
// global scope
let x = 1;

const outerFunc = () => {
    // local scope
    let y = 2;

    console.log(x);
    console.log(y); 

    const innerFunc = () => {
        console.log(x += 5)
        console.log(y += 2) 
    }

    return innerFunc;
}

const result = outerFunc();
```

##### Output
```js
1 // x
2 // y
```
This time, console logs in ```innerFunc``` has not been executed. Rather `innerFunc` has been returned by the `outerFunc` and the ```result``` variable contains the ```innerFunc```.<br>
So now, even after execution of `outerFunc`, we can call ```innerFunc``` by calling ```result()``` and this `innerFunc` can access it's parent functions variable. 

```js
result();
```
##### Output
```js
6 // updated x by innerFunc
4 // updated y by innerFunc
```
Here, ```result()``` containing the ```innerFunc```, accessing the variable ``y`` declared in ```outerFunc``` along with global variable `x`. Even though, ```outerFunc``` has already been executed.
<h4 style=color:green> This ability of a function is called CLOSURE</h4>

This is not just for one time call only. Rather calling `result()` multiple times, will also update the value.

```js
result();
result();
result();
```
##### Output
```js
6 // x
4 // y
11 // x
6 // y
16 // x
8 // y
```

Each time calling the `result()` invoke `innerFunc` and that `innerFunc` access the variables.

#### Questions

What will log to console the following code snippet:
```js
let count = 0;
(function immediate() {
  if (count === 0) {
    let count = 1;
    console.log(count); // What is logged?
  }
  console.log(count); // What is logged?
})();
```

##### Answer

```js
1
0
```

What will log to console the following code snippet:

```js
for (var i = 0; i < 3; i++) {
  setTimeout(function log() {
    console.log(i); // What is logged?
  }, 1000);
}
```
##### Answer

```js
3
3
3
```
What will log to console the following code snippet:
```js
function createIncrement() {
  let count = 0;
  function increment() { 
    count++;
  }
  let message = `Count is ${count}`;
  function log() {
    console.log(message);
  }
  
  return [increment, log];
}
const [increment, log] = createIncrement();
increment(); 
increment(); 
increment(); 
log(); // What is logged?
```

##### Answer

```js
Count is 0
```

