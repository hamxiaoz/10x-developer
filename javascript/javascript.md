# JavaScript

JavaScript = ECMAScript + DOM \(`window.document`\) + BOM \(`window.document, window.navigator, window.location, window.history, window.screen, etc`\)

Good Tutorials

* [https://javascript.info/](https://javascript.info/)

## Type

JavaScript Types = Primitive types + Reference Type

Primitive type

* `null, undefined, boolean, number, string, symbol (ES6)`
* immutable, fixed size memory

Reference Type

* `Object, array, function`
* dynamic size

`typeof` returns string.

## Array

```javascript
var a = Array(4); // array length of 4, but elements are all undefined
var a = Array('4'); // returns [4]
var a = Array()
var a = Array('a', 'b');
var a = ['a', 'b']
let arr = Array.from($('a')); // create from nodelist
```

* can change length, like C\# list: `a.push('c')`
* can hold **different** data type
* the length of the array is one more than the highest index. it's not **always** counting how many members in the array!

  ```text
  var arr = ['a', 'b', 'c'];
  arr.length // 3
  arr[100] = '100'
  arr.length == 101 // !!!`
  ```

* If you query a non-existent array index, you get `undefined`

Callback is usually: `element, index, array` while `element` is required

Value Most of the operations will **mutate** the array.

* copy itself to itself, \[start, end\) not including the endIndex: `copyWithin(targetIndex, startIndex, endIndex)`
* Reverse:   `Array.prototype.reverse()`
* Sort: `arr.sort()`
  * if no function is provided, element is **converted to string** to sort, so `[10, 5].sort() is still [10, 5]`
  * sort numbers: `arr.sort((a, b) => a - b);`
* head: `shift()` + `unshift()`
* tail: `pop()`   +  `push()`
* Fill with value, \[start, end\) `arr.fill`
* \*Remove and insert in the middle \(when deleteCount is 0\): `arr.splice(start, deleteCount[, insert args])`, it will return the removed
* **clear content** `arr.length = 0;` or `arr.splice(0, arr.length)`;

**immutable** operation:

* Concat
  * return new array: `arr.concat(arr2)`
    * has flatten effect: `[1].concat(2, [3,4]) -> [1,2,3,4]`
  * We could make it mutating too: **in place \(append b to a\)**: `Array.prototype.push.apply(a,b)`
* Slice, return shallow copy \[start, end\): `arr.slice`

Iterate

* for: `for(let i = 0, l = list.length; i < l; i++) {console.log(list[i]); }`. Use `break` to break out.
* for in `values()`: `for (let elem in arr.values())`
* `arr.forEach`: **cannot break unless throw an exception**

Transform

* filter: `array.filter or _.filter or _.select`
* join to string: `arr.join`
* reduce and reduceRight\(from end\): `arr.reduce(callback, initial) # call back is (accumulator, currentValue, index, array)=> {})`
  * if no initial value given, first call, previousValue is arr\[0\] and currentValue is arr\[1\]

    ```text
    [1,2,3].reduce((acc, cur)=> acc+cur); // 6
    ```

  * the callback function returns value that'll pass to next accumulator. There is no need to assign `acc = acc + cur` in the callback function.

Query/Test

* Check if it's array: `Array.isArray()`
  * polyfill: `return Object.prototype.toString.call(arg) === '[object Array]';`
* Test all: `arr.every((element) => true)` or `_.all or _.every`
* Test some: `arr.some` or `_.some or _.any`
* Find first, else return `undefined`: `array.find or array.findIndex`
* Includes:
  * \(ES7\): `arr.includes or _.contains`
  * `indexOf or lastIndexOf`

Tips:

* create array:
  * ES6: `Array(length).fill().map((_,i)=>i+1)`
  * ES6: `Array.from({length: 10}, (v, i) => i);`
  * Lodash: `_.fill(Array(10), 1);`

## Number

* Special Numbers:
  * `Infinity` and `-Infinity`
  * `NaN`
    * any operation with NaN will rerturn Nan
    * NaN doesn't equal to anything, including itself
* Hex and Octal:
  * If number starts with 0 and is a valid octal number, it'll be a octal number: `var octalNum = 070; // 56`
  * hex number: `var hexNum = 0xA2 or 0xf1`
* Convert anything to number:
  * `Number()`
    * `Number(null) === 0`
    * `Number(undefined) === NaN`
    * `Number('') === 0`
    * `Number('a') === NaN`
    * `Number('0x1') === 1`
  * `parseInt`
    * `parseInt` parses until found invalid character, + simply convert the string to int/float and it returns NaN if there is ANY invalid character.
      * `parseInt('    1') === 1`
      * `parseInt('') === NaN` returns NaN if cannot convert
      * `parseInt('   123abc4') === 123`
    * **always** use radix: `parseInt('09', 10)` Otherwise '09' will be treated as hex and result as 0
  * `paserFloat`
    * It always convert to oct. If starts with 0x, it returns 0.
* Get digits: `String(321)split('')`
* Check if it's integer: `Number.isInteger` [polyfill on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/isInteger)

**Tips: Random number**

* `Math.random()` -&gt; \[0, 1\)

```javascript
function getRandomArbitrary(min, max) {
  return Math.random() * (max - min) + min;
}

function getRandomInt(min, max) {
  min = Math.ceil(min);
  max = Math.floor(max);
  return Math.floor(Math.random() * (max - min)) + min; //The maximum is exclusive and the minimum is inclusive
}
```

**Tips: format number**

link: [https://codesandbox.io/s/js-tips-format-number-frd6v](https://codesandbox.io/s/js-tips-format-number-frd6v)

```text
function formatNumber(num, decimals) {
  if (decimals < 0) {
    throw new Error('Decimals cannot be smaller than 0');
  }

  const factor = Math.pow(10, decimals);
  return Math.round(num * factor) / factor;
}
```

## String

* string is value tpye.

  ```javascript
  var a = 'a';
    a.x = 'x';
    a.x // will be undefined
    var b = new String('b');
    b.x = 'x';
    b.x // will be 'x'
  ```

* It's unicode of 16bit
* `u1235` is unicode nnnn
* `charAt(index), indexOf`
* `match(regex)` returns matches
  * NOTE if regex has /g: 1. it'll return first match; 2. you can match multiple times. See [http://www.2ality.com/2013/08/regexp-g.html](http://www.2ality.com/2013/08/regexp-g.html)
* `replace(regex/g, 'to replace')` specials '$1', etc.
* `substr(index, length) vs substring(index, endIndex)` not including endIndex\`
  * if negative number:
    * `slice(index)` index will become index+length: `'abc'.slice(-1) -> 'abc'.slice(2) -> 'c'`
    * `substr(index, length)` index becomes index+length; length will become 0
    * `substring` will treat negative as 0
* Can mix different type using '+' since JavaScript is weak typed. The non-string type is auto converted to string.
* So, if you add a string to a number \(or other value\) everything is converted in to a string first

  ```text
  this year is " + 2013 => "this year is 2013"
    '3'+4+5 => '345'
    4+5+'3' => '93'
  ```

* To convert to string, use either `toString` or `String()`
  * `String(null) === 'null'`
  * `String(undefined) === 'undefined'`
* In place sort string with numbers: `'8902'.split('').sort().join('')`
* Use `String.prototype.localeCompare()` for string comparison in sort. Return negative number if it's before. You can also use `'A' > 'a'`

### Special reference type: String, Boolean, Number

* it's created on the fly then get destroyed.

  ```javascript
  var a = 'abc';
  a.subString(0); // a is value type, why it has methods?
  // It's doing something like this:
  var tmp = new String('abc');
  var s = tmp.subString(0);
  tmp = null;
  ```

## Date

Only **using new will return the object**; Others will return the number or string.

* `new Date()`
* `new Date(2005, 0, 3)` local time; year and month is required, month is **0 based**
* `Date.UTC(2005, 0, 3)` UTC time; Return number; year and month is required, month is **0 based**
* Use [moment.js](http://momentjs.com/)

  ```javascript
  const now = moment();
  const future = moment('2030-03-30');
  const diffInDays = now.diff(future, 'days');
  ```

## Boolean

Sometimes you'll need to check boolean, it's better to force converting to boolean by:

```javascript
// if you don't do !! you'll get undefined because you're accessing something doesn't exist
const hasMissingChannels = !!this.props.channels.missingChannels && this.props.channels.missingChannels.length > 0;
```

## null undefined

Special objects: `null` and `undefined`

* `null`: a pointer to nothing \(that's why `typeof null === 'object'`. Most case it can be replaced by `undefined`;
* `undefined`: it's like null in other program.
  * If you access a.name and a is {} then it returns `undefined`
  * If arr\[out\_of\_bound\_index\], it returns `undefined`

boolean: any value can be converted to boolean

```javascript
// as false
false
null
undefined
'' //the empty string, for example var thisIsFlase = Boolean('')
0 // the number
NaN // the number

// Anything except the above is true, for example:
'0' // the string
[] // the empty array
{} // the empty object
```

Check is null or empty:

```javascript
function isNullOrEmpty(str) {
    return !str;
}
// if you can use lodash/underscore
function isNullOrEmpty(str) {
    return _.isEmpty(str); // it's actually checking str.length
}

// Be careful with _.isEmpty as it's checking length, so don't use it to check number
_.isEmpty(10) === true;


function isNullOrEmpty(arr) {
    return !arr || arr.length === 0;
}
```

\_.isEmpty\(\):

* check the length of array or string
* CANNOT check number: \_.isEmpty\(10\) === true
* check if object has enumerable own-properties

Check null:

* use `typeof instance.currentPosition  !== 'undefined'`
* Why not using `instance.currentPosition === undefined`? it can [throw error](http://stackoverflow.com/questions/4725603/variable-undefined-vs-typeof-variable-undefined)
* CoffeeScript:
  * coffeescript: ? or ?. \(the latter can soak up so a.address?.zip returns undefined instead of typeerror\)
  * CoffeeScript's existential operator `?` returns true unless a variable is `null` or `undefined`, which makes it analogous to Ruby's nil?

## Comparison

* Equality operator `==`: doesn't compare type, i.e, it converts the type first \(performs type coercion\) then compare

    `"" == false // returns true`

* Strict Equality Operator `===`: doesn't not perform type coercion **recommended**

    `'' == false // return false`

* when comparison includes reference type, the comparison \(both == and ===\) performs pointer comparison.

    `{} != {}`

## Global Objects / Methods

* Set: unique values of any type, `has`
* Map: dictionary, any type can be key, `size`, `get/set`

Methods:

* `isNaN, etc`
* `let id = setTimeout(()=>console.log('future'), 1000)`, `clearTimeout(id)`
* `let id = setInterval(()=>console.log('again'), 1000)`, `clearInterval(id)` Use setTimout to emulate interval, as timeout is pushed to the queue, where interval might run in overlap.
* `window.print` display print window
* `location`: window.location is the same as document.location
* encodeURI
  * replaces all characters except: `; , / ? : @ & = + $ - _ . ! ~ * ' ( ) # a-z 0-9`
* encodeURIComponent 
  * replaces all characters except`- _ . ! ~ * ' ( ) a-z 0-9`
  * Use it to encode the **value** part: because it'll encode `=` and `&` so it's **not** supposed to encode the whole param string `encodeURIComponent("var1=value1&var2=value2")`.

    ```text
    var arr = [];
    for(var i=0;i<256;i++) {
    var char=String.fromCharCode(i);
    if(encodeURI(char)!==encodeURIComponent(char)) {
      arr.push({
        character:char,
        encodeURI:encodeURI(char),
        encodeURIComponent:encodeURIComponent(char)
      });
    }
    }
    console.table(arr);
    ```

## Object

* the property name will always be string, even you created like this `{a:'b'}`
  * Use dot notation when accessing properties
  * Use subscript notation \[\] when accessing properties with a variable.

    ```javascript
    const isJedi = luke.jedi;
    // dynamic
    funciton getProp(obj, prop) { return obj[prop]; }
    const isJedi = getProp(luke, prop);
    ```
* `for (let prop in obj)` will iterate all **enumerable** props \(including the prototype ones\) in **arbitrar** order
  * All properties that we create by simply assigning to them are enumerable. 
  * The standard properties in `Object.prototype` are all nonenumerable. Ex, `toString` is in prototype but it's not enumerable `'toString' in {} // -> true`
  * use `hasOwnProperty(key)` to check if it's in instance

    ```javascript
    for (let name in map) {
    if (map.hasOwnProperty(name)) {
      // ... this is an own property
    }
    }
    ```
* `for (let value of arr)` \(ES6\). It's using iterator \(`next: ()=> {value: x, done: false}`\)
* The `in` operator check if the specified property is in the specified object.

  * use `hasOwnProperty(key)` to check if it's in instance

    \`\`\`js

    let obj = {

    a: 'a'

    };

    console.log\('a' in obj\); // true

  obj.a = undefined; console.log\('a' in obj\); // true

  delete obj.a; console.log\('a' in obj\); // false

  \`\`\`

* `typeof`, check if it's a **basic type plus others**, it only returns those string: 'undefined', 'null', 'boolean', 'string', 'number', 'object', 'symbol', 'function'
  * so `typeof [] === 'object`
  * **BUT** `typeof null === 'object';` See [MDN explanation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/typeof)
  * usage: check method defined in prototype: `if (typeof this.sayName !== 'function')`
* `a instanceof Constructor`, check if it's a **reference type**
  * Use constructor, not string: so `[] instanceof Object`, not 'object'
* \(**TODO**\) Check if an object is a type
  * Why not `instanceof`?
  * Why not `typeof`? Because typeof returns only those 5 types, and array is Object type. For example, `typeof [] === 'object'`, you cannot tell if it's array. [See here](http://web.mit.edu/jwalden/www/isArray.html)

    ```javascript
    function is(type, obj) {
      var clas = Object.prototype.toString.call(obj).slice(8, -1);
      // [object String]
      return obj !== undefined && obj !== null && clas === type;
    }
    is('String', 'test'); // true
    is('String', new String('test')); // true
    ```
* object detection, check if it has property or method

  ```javascript
  if (document.getElementsByName)

        // or
        if (typeof document.getElementsByName === 'function')
        if (typeof document.getElementsByName !== 'undefined')
  ```

* `JSON.stringify(obj, ['fliter', 'list])` can filter
* Custom getter setter:

  ```javascript
  var pile = {
    elements: ["eggshell", "orange peel", "worm"],
    get height() {
      return this.elements.length;
    },
    set height(value) {
      console.log("Ignoring attempt to set height to", value);
    }
  };

  // or
  Object.defineProperty(TextCell.prototype, "heightProp", {
    get: function() { return this.text.length; }
  });
  ```

* FP operations
  * Freeze: `const frozen = Object.freeze(obj)`
  * Create shallow copy:

    ```javascript
    var o = {
      x: 1,
      y: 2
    };

    // in ES2017+, using object spread:
    var p = { ...o };
    p.y = 3;

    // in ES2015+:
    var p = Object.assign( {}, o );
    p.y = 3;
    ```

## Prototype

### Constructor

A constructor is just a function called with `new`.

```javascript
function Paper(type) {
  this.type = type;
}

let note = new Paper('notebook');
```

What happens?

* create new object
* this bound to new object 
* call the constructor function
* return the object

```javascript
// let note = new Paper('notebook');

// ->
let note = {};
Paper.call(note, 'notebook');
return note;
```

### Prototype Chain

* every instance created with the same constructor will share the same prototype: object derived from Object.prototype.
* How to create prototype-less object? \(so that `for .. in` works without check\)

  ```javascript
  let map = Object.create(null);
  console.log("toString" in map); // → false
  ```

Example

```javascript
function Rabiit() {
}
Rabbit.prototype.teeth = "small";
console.log(killerRabbit.teeth); // → small
killerRabbit.teeth = "long, sharp, and bloody";
console.log(killerRabbit.teeth); // → long, sharp, and bloody
```

Prototype chain:

```javascript
// o ---> Object.prototype ---> null
// The newly created object o has Object.prototype as its [[Prototype]]
// o has no own property named 'hasOwnProperty'
// hasOwnProperty is an own property of Object.prototype. 
// So o inherits hasOwnProperty from Object.prototype
// Object.prototype has null as its prototype.
var o = {a: 1};

// b ---> Array.prototype ---> Object.prototype ---> null
// Arrays inherit from Array.prototype 
// (which has methods indexOf, forEach, etc.)
// The prototype chain looks like:
var b = ['yo', 'whadup', '?'];

// f ---> Function.prototype ---> Object.prototype ---> null
// Functions inherit from Function.prototype 
// (which has methods call, bind, etc.)
function f() {
  return 2;
}

var b = Object.create(o);
// b ---> o ---> Object.prototype ---> null
console.log(b.a); // 1 (inherited)
```

### [Inheritence](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/Inheritance)

* call parent constructor
* set prototype to parent prototype

```javascript
function RTextCell(text) {
  TextCell.call(this, text);
}
RTextCell.prototype = Object.create(TextCell.prototype);
RTextCell.prototype.constructor = RTextCell;
```

ES6, it's just syntax sugar, remains prototype based.

```javascript
class Polygon {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
}

class Square extends Polygon {
  constructor(sideLength) {
    super(sideLength, sideLength);
  }
```

## Function

### arguments

* Always has `arguments` \(note it's not `this.arguments`\).
  * `arguments` is a build-in object, it's array like.
  * To convert it to array:
    * `Array.from(arguments)`
    * `const a = [...arguments];`
    * `Array.prototype.slice.call(arguments)`
* Because of 'arguments', there is no function overloading.
* `function.length` required params length
* `Function.prototype.bind(thisArgs, arg1, arg2...)` creates a new function that binds `this` and currying parameters.
  * so 'this' is always 'thisArgs'
  * use when in `setTimeout` callback to refer this, that's also why `=>` in ES6 don't need to bind anymore
* `Funnction.prototype.apply(scope, paramsArray)` and `Function.prototype.call(scope, param1, param2, etc)`
  * **a**pply uses **a**rray
  * **c**all uses **comma**
  * `Math.max.apply(null, [1,10,-1])`
* Assignment makes a copy of the value only if it's a primitive type \(like Number, Boolean, String, etc...\). Otherwise, assignment just copies a reference to the same object \(Object, Array, etc...\). A new object is not created with assignment.

  ```javascript
  var a = {};
    var b = {name:'b'};
    var a = b;
    console.log(a.name == 'b')
  ```

* Arguments are always copied **by value**. Even if the type is reference.

  ```javascript
  function setName(obj) {
        obj.name = 'Andrew';
        obj = new Object(); // local copy of obj now points to new object
        obj.name = 'Bella';
    }

    let obj = {};
    setName(obj);
    console.log(obj.name); // 'Andrew'
  ```

### Return value

* Function output: funciton always return a value. If no return statement or `return;`, it returns `undefined`.

### Declaration vs Expression

Declaration \(will be hoisted\)

```javascript
  alert(sum(10,10));
  function sum(num1, num2) {
      return num1 + num2;
  }

  // error: alert(sum(10,10));
  let sum = function(num1, num2) {
      return num1 + num2;
  };
  alert(sum(10,10));
```

Expression:

```javascript
//anonymous function expression
var a = function() {
    return 3;
}

//named function expression
var a = function bar() {
    return 3;
}

//self invoking function expression
(function sayHello() {
    alert("hello!");
})();
```

IIFE: immediately-invoked function expression

* Why? It's useful when you have some work to do, some initialization maybe. You need to do it only once and you don't want to leave any globals lying around after the work is finished.
* How? It's used to avoid hoisting and creating scope. A function creates a scope.

  ```javascript
    (function(){
    var a = 1;
    var b = 2;
    alert(a + b);
    })();

    // or use a named version
    (function foo() {
      alert('in foo');
    })();
  ```

### Function Name

Why you can pass function name to map function?

```javascript
let getJSON = (url)=>{}
[].map(getJSON); // see getJSON
```

Actually you’re NOT omitting function parenthesis, what you mean here is passing the function reference so that the map knows which function to call. See [http://stackoverflow.com/questions/5520155/settimeout-callback-argument/5520190\#5520190](http://stackoverflow.com/questions/5520155/settimeout-callback-argument/5520190#5520190)

### Closure

Closure: when the inner function makes reference to a variable to the outer/surrounding function, this is called closure.

* More formal definition: A closure = a function + lexical environment within which that function was declared.
* Usage: promise chain, currying function, this-that pattern，'private' data in module or function \(because function creates scope\)

  ```javascript
  function runningCounter(start) {
    var val = start;

    return function current(increment = 1){
        val = val + increment;
        return val;
    };
  }

  var score = runningCounter( 0 );

  score(); // 1
  score(); // 2

  // 'private' data
  let application = (function() {
    let _components = [];

    return {
      getComponentCount: function() {
        return _components.length;
      }
    };
  })();
  ```

Common error when creating closure in loop:

```javascript
// https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures
function showHelp(help) {
  document.getElementById('help').innerHTML = help;
}

function setupHelp() {
  var helpText = [
      {'id': 'email', 'help': 'Your e-mail address'},
      {'id': 'name', 'help': 'Your full name'},
      {'id': 'age', 'help': 'Your age (you must be over 16)'}
    ];

  for (var i = 0; i < helpText.length; i++) {
    var item = helpText[i];
    document.getElementById(item.id).onfocus = function() {
      showHelp(item.help);
    }
  }
}
setupHelp();

// fix: use let to create local scope
```

## Scope

Who can create scope?

* function scope: created by funciton.
  * `var` is limited in the scope.
  * the scope implicitly defines a reference to `this`
* ES6: block scope
  * `let` is local to the block scope, not the function scope.
  * the scope **does not** implicitly defines a reference to `this`
* ES6: lambda scope
  * the scope **does not** implicitly defines a reference to `this`. So `this` refers to enclosing scope.

Declared variable is a property of the scope. Undeclared variable too. So, both `var a = 10; b = 11;` is accessible in global window.

```javascript
var a = 10;
console.log('a' in window); // true
console.log(window.a); // 10

b = 11;
console.log('b' in window); // true
console.log(window.b); // 10
```

for loop:

* `var` creates one binding as well as a variable \(and the declaration part will be hoisted\), so when i is accessed in a callback function, it always refered to the final i value.
* `let` creates binding each iteration so it works normally

```javascript
let arr = [];
for (var i=0; i < 3; i++) {
    arr.push(() => i);
}
console.log(arr.map(x => x())); // [3,3,3]
console.log(i); // 3
```

How does js lookup variable?

* Similar to stack, look for local then global. Local variables 'shallow' the global ones.
* If there is a **local same name identifier**, the search will stop.

Examples:

```javascript
x = "global";

// function scope:
(function() {
    console.log(x); // undefined (x get hoisted, search will stop)

    var x = 'local';
}());

// block scope
{
    console.log(x); // ReferenceError: x is not defined (x get hoisted but it's not initialized)
    let x = 'local';
}
```

## Hoisted

What will be hoisted?

* `var`

  * **only the declaration part**
  * and it'll be initialized as `undefined`

  ```javascript
  console.log(a); // undefined
  var a = 12;

  // will become this:
  var a;
  console.log(a);
  a = 12;
  ```

* function declaration: `function foo() {}`

  ```javascript
  hoisted(); // Output: "This function has been hoisted."

  function hoisted() {
    console.log('This function has been hoisted.');
  };

  // expression is NOT hoisted
  expression(); //Output: "TypeError: expression is not a function

  var expression = function() {
    console.log('Will this work?');
  };
  ```

* `let const`
  * only the delcaration part 
  * it will be **uninitialized**, trying to use it will cause 'Reference error: y is not defined'. 
  * This is _temporal dead zone_ \(anything above the actual statement\). See: [https://stackoverflow.com/a/31222689](https://stackoverflow.com/a/31222689)

## this

Rules:

1. Normally, `this` is bind to 'Call-site', the invoking object.
2. In arrow function, `this` is bind to the context 'Where is defined'. If no parent defines [scope](javascript.md##Scope), then the context is `window`
3. You can use `bind` to change `this` manually.
4. in event handler, `this` is bind to invoking target. \(NOTE if you define event handler using arrow function then it's bind to window\)

Examples:

* Normally, 'this' is the invoking object. If no invoking object, is the global object. \(window or global in Node\).

  ```javascript
  //
  // Test
  //
  function speak(line) {
    console.log(this.type);
  }
  let a = {type: "white", speak: speak};
  a.speak(); // white

  //
  // test
  //
  // this binds to window, because it's defined when executing
  Vector.prototype.plus = (other)=> { 
    return new Vector(this.x + other.x, this.y + other.y);
  }

  //
  // test
  //
  var global = function(){ console.log(this); }();
  // 立即执行函数，由于没有给他object，于是this就是global (window)

  //
  // test
  //
  function Foo() {
  }
  Foo.method = function() {
    function point(x, y) {
      console.log(this);
      this.x = x;
      this.x = y;
    }
    point(3,5); 
  }
  // this is window.
  // Why? because Foo is defined in window.
  Foo.method();
  ```

* When using `bind`, `this` is set to a fixed value when **it's defined**. Or use `apply` or `call` to dynamically change context.
* Arrow function doesn't bind `this`, `arguments`.
* Arrow function `this` is determined by **where is defined**. And it refers to the enclosing execution context. You can think it's using the this-that pattern. \(Can use babel to verify\) 箭头函数从封闭它的（函数或全局）作用域采用 this 绑定.

  ```javascript
  // test
  // Why? Code executed by setTimeout() is called from an execution context separate from the function from which setTimeout was called.

  function Person() {
    this.age = 0;

    setInterval(function growUp() {
      // In non-strict mode, the growUp() function defines `this` 
      // as the global object, which is different from the `this`
      // defined by the Person() constructor.
      console.log(this.age);
      this.age++;
    }, 1000);
  }
  var p = new Person();

  // fix
  function Person() {
    this.age = 0;

    setInterval(()=> {
      console.log(this.age);
      this.age++;
    }, 1000);
  }
  var p = new Person();

  // ex
  foo.prototype.say = () => {  
    console.log(this === window); // => true
    // ()=> is defiend in is in window.
  };

  // ex
  var button = document.getElementById('myButton');  
  button.addEventListener('click', () => {  
    console.log(this === window); // => true
  });
  ```

* Arrow function is not suitable to define methods:
* So arrow function cannot be used as constructor, because there is no `this` in it.

  ```javascript
  var obj = {
    i: 10,
    b: () => console.log(this.i, this),
    c: function() {
      console.log(this.i, this);
    }
  }
  obj.b(); // prints undefined, Window {...} (or the global object)
  // Why? it's defiend in obj =, the enclosing context is window.
  obj.c(); // prints 10, Object {...}

  // fix: ES6 shorthand method
  var obj = {
    b() {
      console.log(this.i, this)
    }
  };
  ```

* Default binding. It means binding loss: it happens whenever you’re accessing a method through a reference instead of directly through its owner object.

  * Why? Because the invoking site is window.
  * So it also means, when you pass function as callback \(which implicitly do the assignment in local scope, and when invoking, none is invoking it.\), it's window.
  * How to fix? this-that pattern or arrow function.

  ```javascript
  // test
  let john = {
    name: 'John',
    // test 1
    greet: function(person) {
      console.log("Hi " + person + ", my name is " + this.name);
    },
    items: [1, 2, 3],
    // test 2
    processItems: function() {
      this.items.forEach(function(item) {
        this.markItemAsProcessed(item);
      });
    },
    processed: [],
    markItemAsProcessed: function(item) {
      this.processed.push(item);
    }
  };

  // test 1
  john.greet();
  let fx = john.greet;
  fx("Mark"); // this.name will be referencing global object because fx is property of global, global is the invoking object.

  // test 2
  john.processItems(); // this.markItemAsProcessed is not a function

  // fix: that pattern (using closure)
    processItems: function() {
      let that = this;
      this.items.forEach(function(item) {
        that.markItemAsProcessed(item);
      });
    },
  // fix: arrow function
    processItems: function() {
      this.items.forEach((item)=> {
        this.markItemAsProcessed(item);
      });
    },

  // other examples

  // ex
  function foo() {
    setTimeout(() => {
      console.log('id:', this.id);
    }, 100);
  }
  var id = 21;
  foo(); // id: undefined ()=> is defined in foo(), which is defined in window
  foo.call({id: 42}); // id: 42

  // ex
  function Timer() {
    this.s1 = 0;
    this.s2 = 0;
    setInterval(() => this.s1++, 1000);
    setInterval(function () {
      this.s2++;
    }, 1000);
  }
  var timer = new Timer();
  setTimeout(() => console.log('s1: ', timer.s1), 3100); // 3 (new Timer() defines this for arrow function, and it's the function scope)
  setTimeout(() => console.log('s2: ', timer.s2), 3100); // 0 (this is the invoking scope)
  ```

Reference:

* [https://github.com/getify/You-Dont-Know-JS/blob/1ed-zh-CN/this %26 object prototypes/ch2.md](https://github.com/getify/You-Dont-Know-JS/blob/1ed-zh-CN/this%20%26%20object%20prototypes/ch2.md)
* [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this)
* [http://es6.ruanyifeng.com/\#docs/function\#箭头函数](http://es6.ruanyifeng.com/#docs/function#箭头函数)

## Error Exception

* catch: there is no selective catch. `catch(e)`
* You can create your own error and use `instanceOf Constructor`

  ```javascript
  catch (e) {
    if (e instanceof InputError)
      console.log("Not a valid direction. Try again.");
    else
      throw e;
  }
  ```

* Assertion

  ```javascript
  function AssertionFailed(message) {
    this.message = message;
  }
  AssertionFailed.prototype = Object.create(Error.prototype);

  function assert(test, message) {
    if (!test)
      throw new AssertionFailed(message);
  }

  assert(1 === 2, 'msg');
  ```

## i18n

* `navigator.languages` returns the user's preferred languages `//["en-US", "zh-CN", "ja-JP"]`
* `navigator.language` is the first element of the above returned array

### How to test?

Use chrome://settings/languages\#lang and \(important\) make sure that the language you selected is the top choice \(the preferred language\). The navigator value will change accordingly

## Pattern

### default value if it doesn't exist

Use ES6 default parameter instead. Previously: Use \|\| NOTE this pattern doesn't work if the value is ''.

```javascript
for timestamp, count of json["#{projectName}"]
      existing = total["#{timestamp}"] || 0
      total["#{timestamp}"] = existing + count
```

### Console & Debug

`debugger;`

If the result is 0, the elements are not in the DOM: `console.log($(".theElements").length);`

\_ Debug JQuery: [http://fixingthesejquery.com/\#slide23](http://fixingthesejquery.com/#slide23)

### How to open a new window without being blocked?

If the window is not a user click resullt, it'll be blocked.

```text
var win = window.open('', 'Window Name'); // given a name so it'll always refresh this window instead of opening new every time.
win.document.body.innerHTML = '<p>loading...</p>';

// do async work
async.do().then(()=> {
  // Replace the content
  win.document.body.innerHTML = images;
  win.focus();
});
```

Reference:

* [http://stackoverflow.com/questions/2587677/avoid-browser-popup-blockers](http://stackoverflow.com/questions/2587677/avoid-browser-popup-blockers)
* [http://stackoverflow.com/questions/4602964/how-do-i-prevent-google-chrome-from-blocking-my-popup](http://stackoverflow.com/questions/4602964/how-do-i-prevent-google-chrome-from-blocking-my-popup)
* [https://developer.mozilla.org/en-US/docs/Web/API/Window/open](https://developer.mozilla.org/en-US/docs/Web/API/Window/open)

### How to read binary file from the browser?

[https://github.com/jDataView/jDataView](https://github.com/jDataView/jDataView)

