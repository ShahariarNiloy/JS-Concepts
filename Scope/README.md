# Scope

#### According to MDN
> The scope is the current context of execution in which values and expressions are "visible" or can be referenced. If a variable or expression is not in the current scope, it will not be available for use.

#### According to W3Schools
> Scope determines the accessibility (visibility) of variables.

**Scope** is basically the limit. Where variables/functions can and cannot be accessed. The availability of variables and functions in specific areas of the code is referred to as scope. Scopes can also be nested in a hierarchical fashion, so that child scopes can access parent scopes but not vice versa.

JavaScript has 3 types of scope:

1. Block scope
2. Function scope
3. Global scope

#### Block Scope
JavaScript had only Global Scope and Function Scope before ES6 (2015). `let` and `const` are two essential new JavaScript keywords introduced by ES6.
**Block Scope**** is provided by these two keywords in JavaScript.
Variables declared within a `{ }` block cannot be accessible from the outside.

```js

{
  let   x = "Anything";
  const y = "Anything";

  // x & y can be used here. ✅✅
}
// x & y can NOT be used here. ❌❌

{
  let   x = "Anything";
  const y = "Anything";
  {
    // x & y can also be used here. ✅✅ 
  }
}
```

**Block Scope** cannot be applied to variables specified with the `var` keyword. Variables specified inside a `{ }` block can be accessed from the outside.

```js
{
  var x = "Anything";
}
// x can be used here ✅✅ 
```


#### Function Scope
JavaScript has function scope, which means that each function creates a new scope. Variables declared within a function are not visible or accessible from outside the function.

When declared inside a function, variables declared with `var`, `let`, and `const` behave quite similar. They all have the same Function Scope.

```js
function myFunction() {
  var   x = "Anything";
  let   y = "Anything";
  const z = "Anything";

  // x, y & z can only accessible within this function. ✅✅
}
// x, y & z can not be accessible outside of this function. ❌❌

```

#### Global Scope
A variable declared outside the scope of any function or block becomes **GLOBAL**. `var`, `let` & `const` all three follows the same behavior.

```js
var x = "Anything";
let y = "Anything";
const z = "Anything"
// x, y & z can be accessible here. ✅✅

function myFunction() {
// x, y & z can also be accessible here. ✅✅

    {
        // x, y & z can be accessible even here. ✅✅
    }
}
```

#### Question

What will be the output of the three log statements and in what order?
```js
(() => {
  let one, two;
  try {
    throw new Error(321);
  } catch (one) {
    (one = 123), (two = 321);
    console.log(one);
  }
  console.log(one);
  console.log(two);
})();
```

##### Answer

```js
123
undefined
321
```