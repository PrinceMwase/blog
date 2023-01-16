---
title: "Understanding Variable Scope in Javascript"
date: 2023-01-16T10:22:33+02:00
draft: false
---

JavaScript, like many programming languages, has a specific way of handling the scope of variables. In this article, we will take a closer look at variable scope in JavaScript and how it works.

## What is Variable Scope?

In programming, a variable's scope refers to the portion of the code where the variable can be accessed. There are two types of variable scope in JavaScript: global and local.

## Global Scope

A variable declared outside of any function or block has global scope. This means that it can be accessed and modified from any part of the code, including inside functions and blocks.

``` javascript
    let globalVariable = "I am a global variable";

    function myFunction() {
    console.log(globalVariable);  // Output: "I am a global variable"
    }

    myFunction();
    console.log(globalVariable);  // Output: "I am a global variable"
```

## Local Scope

A variable declared inside a function or block has local scope. This means that it can only be accessed and modified from within the function or block where it was declared.

``` javascript
    function myFunction() {
    let localVariable = "I am a local variable";
    console.log(localVariable);  // Output: "I am a local variable"
    }

    myFunction();
    console.log(localVariable);  // ReferenceError: localVariable is not defined
```

## Block Scope

JavaScript also has block scope which is created by a block statement ({ }). Variables declared with `let` or `const` inside a block statement can only be accessed within that block. Variables declared with `var` have function scope, so they can be accessed inside and outside of the block.

```javascript
    if (true) {
    let blockScopeVariable = "I am a block scope variable";
    console.log(blockScopeVariable);  // Output: "I am a block scope variable"
    }
    console.log(blockScopeVariable); // ReferenceError: blockScopeVariable is not defined
```

## Hoisting

JavaScript has a behavior called hoisting, which means that variable and function declarations are moved to the top of the code before execution.

``` javascript
    console.log(hoistedVariable); // Output: undefined
    var hoistedVariable = "I am a hoisted variable";

    console.log(hoistedFunction()); // Output: "I am a hoisted function"
    function hoistedFunction() {
    return "I am a hoisted function";
    }
```

In the example above, the variable `hoistedVariable` and the function `hoistedFunction` are hoisted to the top of the code before execution. This means that they can be accessed and called before they are declared in the code. However, it's important to note that hoisting only applies to variable and function declarations, and not their assignments. This means that trying to access a variable before it is assigned a value will return `undefined`.

Understanding variable scope in JavaScript is crucial for writing efficient and maintainable code. You can better control the accessibility of your variables and avoid potential bugs. Remember to always consider the scope of your variables when declaring and using them in your code.

____________________________________________________________________________________________________________________________

###### Written by Prince Mwase