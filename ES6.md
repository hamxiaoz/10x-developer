# ES6

References:
- http://exploringjs.com/es6/ch_modules.html
- http://es6.ruanyifeng.com/
- Coffeescript to ES6:
    - https://gist.github.com/danielgtaylor/0b60c2ed1f069f118562
    - https://robots.thoughtbot.com/replace-coffeescript-with-es6
    
## Iterate
- JavaScript原有的for...in循环，只能获得对象的键名，不能直接获取键值: Iterate over property name:

```js
for (let prop in obj) {
}

// use Object.keys
Object.keys(obj).forEach(function (key, index) {
    console.log(obj[key]);
}

// underscore
_.keys(obj, function (value, key) {
});
```

CoffeeScript -> ES6:

```js
// coffee
for prop, value of obj

// ES6
_.keys(obj, (value, key)=>{
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
_.keys(arr, function (element, index) {
});
```

CoffeeScript -> ES6:

```js
// coffee
for ele in arr
    console.log ele
    
// es6
for (let ele of arr) {
    console.log(ele);
}

// or
arr.forEach( (ele) => {
    console.log(ele);
    //  函数体内的this对象，就是定义时所在的对象，而不是使用时所在的对象
});

arr.forEach(function(ele){
    console.log(ele);
    //  this is the function
});
```

- 

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

### Block
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