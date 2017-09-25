---
layout: post
title:  "Learning Node.js"
date:   2017-09-11 02:11 +0800
categories: nodejs
excerpt_separator: <!--more-->
---
# Node.js
> Node.js is a JavaScript runtime built on Chrome's V8 JavaScript engine. 

We will try to learn the basics of node.js in this post. We'll talk about what, why and how it works and how to install it. We're also gonna try to build our own simple module using node.js and publish it 
<!--more-->
### What is Typescript?
Typescript is a typed superset of Javascript that compiles to plain Javascript.

### Installing / Getting started
> Using an acer laptop (e5-573) with Windows 7 while doing the installation.

There are two main ways of installing typescript. 
1. Via NPM.
2. Using Visual Studio 2017

Via NPM. 
```shell
$ npm install -g typescript 
```

### Prerequisites
> Basic understanding of javascript programming concepts

### Compiling your code 
At the command line, run the TypeScript compiler.
```shell
$ tsc yourfile.ts
```

This will create a new javascript file which contains the same JavaScript you fed in. 

### Basic Types 
1. Boolean = True/false
2. Number = Decimal/Hex/Binary/Octal
3. String = Textual Types/""/''
4. TemplateStrings = Multiple lines using backticks ``
5. Array = []
6. Generic Array Type = Array<string/ElemType>
7. Tuple = Fixed number of elements/[string,number]
8. Enum = Color {Red, Green, Blue } |  let c: Color = Color.Green
9. Any = for type-checking 
10. Void = Declaring variables of type void is not useful because you can only assign undefined or null to them:
11. Null/Undefined = Much like void, they’re not extremely useful on their own.
12. Never: never is the return type for a function expression or an arrow function expression that always throws an exception or one that never returns.
13. TypeAssertion = let strLength: number = (<string>someValue).length. 




### Type Annotation
Type annotations in TypeScript is a way to record the intended contract of a function or variable. In this case we made the greeter function called with a sing string parameter.

```javascript
funtion greeter(person: string) {
    return "Hello" + person;
}

var user = "Jane User"
document.body.innerHTML = greeter(user);
```

### Interfaces 



