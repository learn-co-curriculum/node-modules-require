# Importing, and Exporting Modules in Node

## Overview

This lesson will cover how to import and export modules in Node.js, what syntax and operators to use and highlight the differences between browser JavaScript and Node when it comes to modules.

## Objectives

1. Describe syntax for working with Node modules
1. Describe export
1. Describe require
1. Describe relationship to CommonJS (contrast with ES6 and browser modules)

## Modules

Modules are distinct chunks of logic typically combined by their functionality (by their purpose). For example, if you are building a date picker, you might want to abstract (separate into a module) your date picker logic into a separate component/package/module, because the chances are very high that you'll need more than one date input field: data of birth, date of expiration on a credit/debit card, date of delivery, etc.

Writing modular code is the best practice because the more you can re-use the old code from other parts of the application in a new features and places, the better the overall project will be. There is one tiny problem with browser JavaScript however—it doesn't have built-in modules! That is insane if you think about it. Developers have to use HTML which is another language to include browser JavaScript files. But even then, the dependency management is awful and the `<script>` tags are often blocking the loading of other resources (they are synchronous).

Ingenuity of the JavaScript community led to the invention of various JavaScript-only approaches to modules such as CommonJS, RequireJS, and AMD. Under the hood, these standards and libraries used AJAX (Asynchronous JavaScript and XML) or XHR to fetch other JavaScript libraries/modules. Not ideal, but works better than having to manage 100s of `<script>` tags.

Of course, creators of Node.js new about this issue. They implemented CommonJS notation for the module system. It's very simple and elegant. 

## Syntax for Working with Node Modules

How do you get started with modules in Node? Simple. All you need to do is use `require` for importing from a main file, and `module.exports` for exporting in the module.

Consider monolithic code (the code which has all the logic in it) which outputs hello in different languages:

```js
var sayHelloInEnglish = function() {
  return 'Hello'
}

var sayHelloInTatar = function() {
  return 'Isänmesez'
}

console.log("Tatar " +
  sayHelloInTatar() +
  " & English " +
  sayHelloInEnglish())
```




## Resources

1. []()
1. []()
1. []()


---

<a href='https://learn.co/lessons/node-modules-require' data-visibility='hidden'>View this lesson on Learn.co</a>
