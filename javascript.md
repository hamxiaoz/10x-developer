# JavaScript

JavaScript = ECMAScript + DOM (`window.document`) + BOM (`window.document, window.navigator, window.location, window.history, window.screen, etc`)


- [Type](#type)
- [Array](#array)
- [Number](#number)
- [String](#string)
- [Date](#date)
- [boolean](#boolean)
- [Object](#object)
- [null undefined](#null-undefined)
- [Comparison](#comparison)
- [Map Set](#map-set)
- [Global Object](#object)
- [Function](#function)
- [Pattern](#pattern)

## Type

JavaScript Types = Primitive types + Reference Type

Primitive type
  - `null, undefined, boolean, number, string, symbol (ES6)`
  - immutable, fixed size memory

Reference Type
  - `Object, array, function`
  - dynamic size

`typeof` returns string.

## Array

```js
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
      var arr = ['a', 'b', 'c'];
      arr.length // 3
      arr[100] = '100'
      arr.length == 101 // !!!`
* If you query a non-existent array index, you get `undefined`

Callback is usually: `element, index, array` while `element` is required

Value
Most of the operations will **mutate** the array.
- copy itself to itself, \[start, end\) not including the endIndex: `copyWithin(targetIndex, startIndex, endIndex)`
- Reverse:   `Array.prototype.reverse()`
- Sort: `arr.sort()`
  * if no function is provided, element is **converted to string** to sort, so `[10, 5].sort() is still [10, 5]`
  * sort numbers: `arr.sort((a, b) => a - b);`
- Remove and return head: `arr.shift()`
- Add item to head: `arr.unshift('a')`
- Fill with value, \[start, end\) `arr.fill`
- *Remove and insert in the middle \(when deleteCount is 0\): `arr.splice(start, deleteCount[, insert args])`, it will return the removed
- **clear content** `arr.length = 0;` or `arr.splice(0, arr.length)`;

**immutable** operation:
- Concat
  * return new array: `arr.concat(arr2)`
    * has flatten effect: `[1].concat(2, [3,4]) -> [1,2,3,4]`
  * We could make it mutating too: **in place \(append b to a\)**: `Array.prototype.push.apply(a,b)`
- Slice, return shallow copy \[start, end\): `arr.slice`

Iterate

* for: `for(let i = 0, l = list.length; i < l; i++) {console.log(list[i]); }`. Use `break` to break out.
* for in `values()`: `for (let elem in arr.values())`
* `arr.forEach`: **cannot break unless throw an exception**

Transform

* filter: `array.filter or _.filter or _.select`
* join to string: `arr.join`
* reduce and reduceRight\(from end\): `arr.reduce(callback, initial) # call back is (previousValue, currentValue, index, array)=> {})`
  * if no initial value given, first call, previousValue is arr\[0\] and currentValue is arr\[1\]
    ```
    [1,2,3].reduce((pre, cur)=> pre+cur); // 6
    ```

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
- create array:
  - ES6: `Array(length).fill().map((_,i)=>i+1)`
  - ES6: `Array.from({length: 10}, (v, i) => i);`
  - Lodash: `_.fill(Array(10), 1);`

## Number

- Special Numbers:
  - `Infinity` and `-Infinity`
  - `NaN`
    - any operation with NaN will rerturn Nan
    - NaN doesn't equal to anything, including itself
- Hex and Octal:
  - If number starts with 0 and is a valid octal number, it'll be a octal number: `var octalNum = 070; // 56`
  - hex number: `var hexNum = 0xA2 or 0xf1`
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

## String

* string is value tpye.
  ```js
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
  ```
  this year is " + 2013 => "this year is 2013"
    '3'+4+5 => '345'
    4+5+'3' => '93'
  ```
* To convert to string, use either `toString` or `String()`
  * `String(null) === 'null'`
  * `String(undefined) === 'undefined'`
* In place sort string with numbers: `'8902'.split('').sort().join('')`

### Special reference type: String, Boolean, Number

* it's created on the fly then get destroyed.
  ```js
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
  ```js
  const now = moment();
  const future = moment('2030-03-30');
  const diffInDays = now.diff(future, 'days');
  ```

## Boolean

Sometimes you'll need to check boolean, it's better to force converting to boolean by:

```js
// if you don't do !! you'll get undefined because you're accessing something doesn't exist
const hasMissingChannels = !!this.props.channels.missingChannels && this.props.channels.missingChannels.length > 0;
```

## Object

* the property name will always be string, even you created like this `{a:'b'}`

  * Use dot notation when accessing properties
  * Use subscript notation \[\] when accessing properties with a variable.

    ```js
    const isJedi = luke.jedi;
    // dynamic
    funciton getProp(obj, prop) { return obj[prop]; }
    const isJedi = getProp(luke, prop);
    ```

* `for .. in` will iterate all enumerable props \(including the prototype ones\) in arbitrar order

  * use `hasOwnProperty(key)` to check

* The [`in` operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/in) returns true if the specified property is in the specified object.

* `typeof`, check if it's a **basic type plus others**, it only returns those string: 'undefined', 'null', 'boolean', 'string', 'number', 'object', 'symbol', 'function'

  * so `typeof [] === 'object`
  * **BUT** `typeof null === 'object';` See [MDN explanation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/typeof)
  * usage: check method defined in prototype: `if (typeof this.sayName !== 'function')`

* `a instanceof Constructor`, check if it's a **reference type**
  * Use constructor, not string: so `[] instanceof Object`, not 'object'
* \(**TODO**\) Check if an object is a type

  * Why not `instanceof`?
  * Why not `typeof`? Because typeof returns only those 5 types, and array is Object type. For example, `typeof [] === 'object'`, you cannot tell if it's array. [See here](http://web.mit.edu/jwalden/www/isArray.html)

    ```js
    function is(type, obj) {
      var clas = Object.prototype.toString.call(obj).slice(8, -1);
      // [object String]
      return obj !== undefined && obj !== null && clas === type;
    }
    is('String', 'test'); // true
    is('String', new String('test')); // true
    ```

* object detection, check if it has property or method

  ```js
  if (document.getElementsByName)

        // or
        if (typeof document.getElementsByName === 'function')
        if (typeof document.getElementsByName !== 'undefined')
  ```

* `JSON.stringify(obj, ['fliter', 'list])` can filter

* [`defineProperty`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty) can set 'writable' and custom setter/getter

* FP operations
 - Freeze: `const frozen = Object.freeze(obj)`
 - Create shallow copy:
    ```js
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


## null undefined

Special objects: `null` and `undefined`

* `null`: a pointer to nothing \(that's why `typeof null === 'object'`. Most case it can be replaced by `undefined`;
* `undefined`: it's like null in other program.
  * If you access a.name and a is {} then it returns `undefined`
  * If arr\[out\_of\_bound\_index\], it returns `undefined`

boolean: any value can be converted to boolean

```js
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

```js
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

## Map Set

* Set: unique values of any type
* Map: dictionary, any type can be key, `size`, `get/set`

## Global Object

Methods:

* `isNaN, etc`
* `encodeURI()` replace space to %20
* `encodeURIComponent()` replace space and others such as '/' and '.', so don't use it for uri, only use it for uri component \(thus its name\)
* `let id = setTimeout(()=>console.log('future'), 1000)`, `clearTimeout(id)`
* `let id = setInterval(()=>console.log('again'), 1000)`, `clearInterval(id)` Use setTimout to emulate interval, as timeout is pushed to the queue, where interval might run in overlap.
* `window.print` display print window
* `location`: window.location is the same as document.location

## Function

### Parameter
* Always has `arguments` (note it's not `this.arguments`).
  - `arguments` is a build-in object, it's array like.
  - To convert it to array:
    - `Array.from(arguments)`
    - `const a = [...arguments];`
    - `Array.prototype.slice.call(arguments)`
* Because of 'arguments', there is no function overloading.
* `function.length` required params length
* `Function.prototype.bind(thisArgs, args)` creates a new function that, when called, has its this keyword set to the provided value, with a given sequence of arguments preceding any provided when the new function is called.
  * so 'this' is always 'thisArgs'
  * use when in `setTimeout` callback to refer this, that's also why `=>` in ES6 don't need to bind anymore
* `Funnction.prototype.apply(scope, paramsArr)` apply takes array as second args: **a**pply/**a**rray
* `Function.prototype.call(scope, param1, param2)` the fundamental difference is that call\(\) accepts an argument list, while apply\(\) accepts a single array of arguments.
* Assignment makes a copy of the value only if it's a primitive type \(like Number, Boolean, String, etc...\). Otherwise, assignment just copies a reference to the same object \(Object, Array, etc...\). A new object is not created with assignment.

  ```js
  var a = {};
    var b = {name:'b'};
    var a = b;
    console.log(a.name == 'b')
  ```

* Arguments are always copied **by value**. Even if the type is reference.

  ```js
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
Declaration (will be hoisted)
```js
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
```js
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
- Why? It's useful when you have some work to do, some initialization maybe. You need to do it only once and you don't want to leave any globals lying around after the work is finished.
- How? It's used to avoid hoisting and creating scope. A function creates a scope.
  ```js
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

### Closure
Closure: when the inner function makes reference to a variable from the outer function, this is called closure.
  ```javascript
  function runningCounter(start) {
    var val = start;

    return function current(increment = 1){
        val = val + increment;
        return val;
    };
  }

  var score = runningCounter( 0 );

  score();                // 1
  score();                // 2
  ```

- Usage: promise chain, currying function.

### Scope

Who can create scope?
- funciton creates scope. `var` is limited in the scope.
- ES6: `let` creates variable that's local to the **block** scope, not the function scope.

How does js lookup variable?  
Similar to stack, look for local then global.

### Hoisted

What will be hoisted?
- `var` (**only the declaration part**)
  ```js
  console.log(a); // undefined
  var a = 12;

  // will become this:
  var a;
  console.log(a);
  a = 12;
  ```

- function declaration: `function foo() {}`
  ```js
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

### this

---


## Pattern

### default value if it doesn't exist

Use ES6 default parameter instead.
Previously: Use \|\|   NOTE this pattern doesn't work if the value is ''.

```js
for timestamp, count of json["#{projectName}"]
      existing = total["#{timestamp}"] || 0
      total["#{timestamp}"] = existing + count
```

### Console & Debug

`debugger;`

If the result is 0, the elements are not in the DOM:
 `console.log($(".theElements").length);`

\_ Debug JQuery: [http://fixingthesejquery.com/\#slide23](http://fixingthesejquery.com/#slide23)

### How to open a new window without being blocked?

If the window is not a user click resullt, it'll be blocked.

```
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

