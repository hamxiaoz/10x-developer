# ES6
References:
- http://exploringjs.com/es6/ch_modules.html
- http://es6.ruanyifeng.com/
- https://github.com/lukehoban/es6features

## Class

```js
class Point {
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }

  toString() {
    return '(' + this.x + ', ' + this.y + ')';
  }
}
```

## Style Guide
Guide: https://github.com/airbnb/javascript

- DON'T use 'single var pattern'
    ```js
    // good
    const items = getItems();
    const goSportsTeam = true;
    const dragonball = 'z';
    ```

- new line
    ```js
    $second
        .on('click',function(){ alert('hello everybody');})
        .fadeIn('slow')
        .animate({height:'120px'},500);
    // vs 
    $second.on('click',function(){ alert('hello everybody');}).
        fadeIn('slow').
        animate({height:'120px'},500);
    // vs
    $second.on('click',function(){ alert('hello everybody');})
        .fadeIn('slow')
        .animate({height:'120px'},500);
    ```
    
- Don't use parentheses for unary operator such as `delete, void, typeof`
- Use single quote '' for strings
- Use function declarations instead of function expressions.


## How to run ES6 in Node
- https://cnodejs.org/topic/56460e0d89b4b49902e7fbd3
- http://blog.andrewray.me/how-to-use-es6-in-nodejs/

index.js
```js
require('babel-core/register');
require('./es6code');

// To run this file, do
// `node index.js`
```

es6code.js
```js
import path from 'path';
class car {
  startEngine() {
    console.log('Ignition on');
  }
}
```

    
## Iteration
- `for...in`: Iterate over property name, **in arbitrary order (because property doesn't have order)**

```js
for (let prop in obj) {
  // Check, in case prototype has customized properties
  if (obj.hasOwnProperty(prop) {
    // ...
  }
}

// when using in array, it iterates on index
// Don't use this
for (let index in arr) {
}

// use Object.keys
Object.keys(obj).forEach(function (key, index) {
    console.log(obj[key]);
}

// underscore
_.each(obj, function (value, key) {
});
```

- ES6: Iterate over values: `for .. of`
 
```js
for (let value of arr) {
}

// use forEach
arr.forEach(function (element, index) {
    console.log(element); 
});

// underscore
_.each(arr, function (element, index) {
});
```


## Module

http://exploringjs.com/es6/ch_modules.html

### ES5
**CommonJS** Modules: The dominant implementation of this standard is in Node.js (Node.js modules have a few features that go beyond CommonJS). Characteristics:
- Compact syntax
- Designed for synchronous loading
- Main use: server

**Asynchronous Module Definition (AMD)**: The most popular implementation of this standard is RequireJS. Characteristics:
- Slightly more complicated syntax, enabling AMD to work without eval() (or a compilation step).
- Designed for asynchronous loading
- Main use: browsers

### ES6
Declarative syntax (for importing and exporting)

```js
//------ lib.js ------
export const sqrt = Math.sqrt;
export function square(x) {
    return x * x;
}
export function diag(x, y) {
    return sqrt(square(x) + square(y));
}

// import
import { square, diag } from 'lib';
console.log(square(11)); // 121
console.log(diag(4, 3)); // 5

// import whole module
import * as lib from 'lib';
console.log(lib.square(11)); // 121
console.log(lib.diag(4, 3)); // 5

// import from node package
import fs from 'fs';
```

Default exports
If you want to export only a single function, you have to use `export default` then you can do `import a from 'MyClass'`
```js
export default function () { ··· } // no semicolon!

//------ main1.js ------
import myFunc from 'myFunc';
myFunc();

// class

//------ MyClass.js ------
export default class MyClass { ··· } // no semicolon!

// or 
export { MyClass };

//------ main2.js ------
import {MyClass} from 'MyClass';
let inst = new MyClass();
```

Programmatic loader API: to configure how modules are loaded and to conditionally load modules


## Block / Scope
- ES5只有全局作用域和函数作用域，没有块级作用域
- ES6: let实际上为JavaScript新增了块级作用域; 函数本身的作用域，在其所在的块级作用域之内。

```js
// 内层作用域可以定义外层作用域的同名变量。

{{{{
  let insane = 'Hello World';
  {let insane = 'Hello World';}
}}}};

// 立即执行匿名函数（IIFE）不再必要了
// IIFE写法
(function () {
  var tmp = ...;
  ...
}());

// 块级作用域写法
{
  let tmp = ...;
  ...
}

// ES6也规定，函数本身的作用域，在其所在的块级作用域之内。
```

## Spread/Rest

Use for collect the rest:

```js
let { x, y, ...z } = { x: 1, y: 2, a: 3, b: 4 };
x; // 1
y; // 2
z; // { a: 3, b: 4 }
```

Use for spread object or array into parameters like:

- shape: {a, b} -> a, b
- shape: [a, b] -> a, b

```js
let n = { x, y, ...z };
n; // { x: 1, y: 2, a: 3, b: 4 }

Math.max(...[1,2,3]);
```
