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

console.log('Tatar ' +
  sayHelloInTatar() +
  ' & English ' +
  sayHelloInEnglish())
```

The code is in the `hello-monolithic.js` and if you run it with `$ node hello-monolithic.js`, you'll see this:

```
Tatar Isänmesez & English Hello
```

So far so good? What if you need to re-use the same hellos in multiple places? Let's abstract (separate the monolithic code into two files) into `greetings.js` (module) and `hello.js` (main file).

The code for the `greetings.js` module  uses `module.exports`:

```
module.exports.sayHelloInEnglish = function() {
  return 'Hello'
}

module.exports.sayHelloInTatar = function() {
  return 'Isänmesez'
}
```

Then in the main file `hello.js`, we import the `greetings.js` with require. Then we invoke the methods like any other functions:

```js
var greetings = require('./greetings.js')

console.log('Tatar ' +
  greetings.sayHelloInSwedish() +
  ' & English ' +
  greetings.sayHelloInEnglish())
```


## Exporting

To export a module, we use `module.exports`. It's a global object meaning there's a property `module` on the `global` object. You can create a property on the `module.exports` object instead of overwriting it completely. 

```js
module.exports.sayHelloInTatar = function() {...}
```

In browser JavaScript, developers have to use global scope to export their modules. For example, jQuery uses this code: 

The way Node works, when you create a file you have two options when it comes to passing the logic between the module and the main file: 

* The `global` object (not recommended)
* Things you export explicitly with `module.exports` (recommended)

Whatever you assign to `module.exports` will be exposed to the main file (the importee). You can export an object, but more often developers prefer to export a function (it's more versatile).

```js
module.exports = {...}
module.exports = function() {...}
```


## Importing

So we have the code neatly organized into separate folder and files for re-use and better development scalability, but how can we use those files from other files (I call the importee or main files)? We use `require()` which is another global method.

Also, you can import many things, not just JS files:

* Node file
* npm module
* Core module
* JSON file
* Folder (really an `index.js` inside of the folder)

You've seen how to import a file in the greetings example, but what about npm and core modules? You just use the name of the module, e.g., for `express` use `require('express')` and for `fs` use `require('fs')`. The difference between core and npm modules is that you need to install the latter with `$ npm install NAME`.

When importing JSON files, you'll get JavaScript/Node object which is convenient. And importing a folder acts as another abstraction. For example, you have 20 utilities files, instead of requiring all 20 in each file, you just include the folder (really an `index.js` which in turn requires and exports the 20 files).

Note: When you import a JavaScript file, Node will execute the code outside of the `module.exports` but not the `module.exports` code.

## Resources

1. [Modules official documentation](https://nodejs.org/api/modules.html)
1. [Node.js, Require and Exports](http://openmymind.net/2012/2/3/Node-Require-and-Exports)
1. [How To Create and Use Node.js Modules video](https://www.youtube.com/watch?v=DZ_bRk8JWDM)
2. [Node.js Modules video](https://www.youtube.com/watch?v=98nlQYgXZGw)


---

<a href='https://learn.co/lessons/node-modules-require' data-visibility='hidden'>View this lesson on Learn.co</a>
