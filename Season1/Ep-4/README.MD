- By Deafault MODULES protects their variables and function from leaking.
- You can not access varibles and functions of a module in another module.
- But if you want then you have to export functions and variables from a module and import those in another module.

- module has two types

  1)common js modules(CJS)=> >module.exports >require() >older way >node.js by default used this>Synchronous way means we can not move forward before excuting that module. >In this code runs in non strict mode means if you are not declaring a varible by let,var and const it still does not give you an error.

  "type":"commonjs"

  2)ES modules(ESM or ES6 module) >import >export >newer way >by Default angular,react used this>Async way which makes it very powerfull >in this code runs in strict mode.

  "type":"module"
