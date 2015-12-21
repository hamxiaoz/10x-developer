## JSON Style Guide
Ref: 
- https://google.github.io/styleguide/jsoncstyleguide.xml

Highlights:
- No comments
- All property names must be surrounded by double quotes
- Property names must be camel-cased, ascii strings. They are always string.

---

## [Underscore](http://underscorejs.org/) and [underscore.string](https://epeli.github.io/underscore.string/)

#### Difference between _.throttle and _.debounce?
https://ruby-china.org/topics/22494
- throttle: At most that fast, usually used when invoking source happens really frequently. Such as when typing to seach, don't send too many requests, scroll, mouse move, etc.
- debounce: wait till no change. Such as calc layout when resize is finished.

#### Convert an object into a list of [key, value] pairs.
```js
_.pairs({one: 1, two: 2, three: 3});
=> [["one", 1], ["two", 2], ["three", 3]]
```

#### how to union with array?
```coffee
a = [1, 2]
b = [3, 4, 5]
c = [6]

console.log _.union(a, b, c)

arr = [a, b, c]
console.log _.union.apply(_, arr)
```

---

## Hows and patterns

JavaScript = ECMAScript + DOM + BOM

### Type: value/ref
- Value type (includes string): `Undefined, Null, Boolean, Number, String`
- Ref type: `function, Object, Array`
- `typeof` returns following string, see below


#### Array
```js
var a = Array(4); // array length of 4, but elements are all undefined
var a = Array('4'); // returns [4]
var a = Array()
var a = Array('a', 'b');
var a = ['a', 'b']
let arr = Array.from($('a')); // create from nodelist
```
- can change length, like C# list: `a.push('c')`
- can hold **different** data type
- the length of the array is one more than the highest index. it's not **always** counting how many members in the array!
```
var arr = ['a', 'b', 'c'];
arr.length // 3
arr[100] = '100'
arr.length == 101 // !!!`
```
- If you query a non-existent array index, you get `undefined`

Callback is usually: `element, index, array` while `element` is required

Value
- **in place** copy itself to itself, [start, end) not including the endIndex: `copyWithin(targetIndex, startIndex, endIndex)`
- Reverse **in place**:   `Array.prototype.reverse()` 
- Sort **in place**: `arr.sort()`
    - if no function is provided, element is **converted to string** to sort, so `[10, 5].sort() is still [10, 5]`
    - sort numbers: `arr.sort((a, b) => a - b);`
- Concat
    - return new array: `arr.concat(arr2)`
        - has flatten effect: `[1].concat(2, [3,4]) -> [1,2,3,4]`
    - **in place (append b to a)**: `Array.prototype.push.apply(a,b)`
- Remove and return head, **mutate**: `arr.shift()`
- Add item to head: `arr.unshift('a')`
- Fill with value, [start, end) `arr.fill`
- Slice, return shallow copy [start, end): `arr.slice`
- Remove and insert (when deleteCount is 0): `arr.splice(start, deleteCount[, insert args])`, it will return the removed

Iterate
- for: `for(let i = 0, l = list.length; i < l; i++) {console.log(list[i]); }`
- values(): `for (let elem in arr.values())`
- Do for each, **cannot break unless throw an exception** `arr.forEach`

Transform
- filter: `array.filter or _.filter or _.select`
- join to string: `arr.join`
- reduce and reduceRight(from end): `arr.reduce(callback, initial) # call back is (previousValue, currentValue, index, array)=> {})`
    - if no initial value given, first call, previousValue is arr[0] and currentValue is arr[1]
    ```
    [1,2,3].reduce((pre, cur)=> pre+cur); // 6
    ```

Query/Test
- Check if it's array: `Array.isArray()`
    - polyfill: `return Object.prototype.toString.call(arg) === '[object Array]';`
- Test all: `arr.every((element) => true)` or `_.all or _.every`
- Test some: `arr.some` or `_.some or _.any`
- Find first, else return `undefined`: `array.find or array.findIndex`
- Includes:
    - (ES7): `arr.includes or _.contains`
    - `indexOf or lastIndexOf`


### number
- If number starts with 0 and is a valid octal number, it'll be a octal number: `var octalNum = 070; // 56`
- hex number: `var hexNum = 0xA2 or 0xf1`
- `NaN`
    - any operation with NaN will rerturn Nan
    - NaN doesn't equal to anything, including itself
- Convert anything to number:
    - `Number()`
        - `Number(null) === 0`
        - `Number(undefined) === NaN`
        - `Number('') === 0`
        - `Number('a') === NaN`
        - `Number('0x1') === 1`
    - `parseInt`
        - `parseInt` parses until found invalid character, + simply convert the string to int/float and it returns NaN if there is ANY invalid character.
            - `parseInt('    1') === 1`
            - `parseInt('') === NaN` returns NaN if cannot convert
            - `parseInt('   123abc4') === 123`
        - **always** use radix: `parseInt('09', 10)` Otherwise '09' will be treated as hex and result as 0
    - `paserFloat`
        - It always convert to oct. If starts with 0x, it returns 0.
- Get digits: `String(321)split('')`
- Check if it's integer: `Number.isInteger` [polyfill on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/isInteger)

### string (value type)
- string is value tpye. 
    ```js
    var a = 'a';
    a.x = 'x';
    a.x // will be undefined
    var b = new String('b');
    b.x = 'x';
    b.x // will be 'x'
    ```
- It's unicode of 16bit
- `u1235` is unicode nnnn
- `charAt(index), indexOf`
- `match(regex)` returns matches
- `replace(regex/g, 'to replace')` specials '$1', etc.
- `substr(index, length) vs substring(index, endIndex)` not including endIndex`
    - if negative number: 
        - `slice(index)` index will become index+length: `'abc'.slice(-1) -> 'abc'.slice(2) -> 'c'`
        - `substr(index, length)` index becomes index+length; length will become 0
        - `substring` will treat negative as 0
- Can mix different type using '+' since JavaScript is weak typed. The non-string type is auto converted to string.
- So, if you add a string to a number (or other value) everything is converted in to a string first
    ```
    this year is " + 2013 => "this year is 2013"
    '3'+4+5 => '345'
    4+5+'3' => '93'
    ```
- To convert to string, use either `toString` or `String()`
    - `String(null) === 'null'`
    - `String(undefined) === 'undefined'`
- In place sort string with numbers: `'8902'.split('').sort().join('')`

### Special reference type: String, Boolean, Number
- it's created on the fly then get destroyed.
```js
var a = 'abc';
a.subString(0); // a is value type, why it has methods?
// It's doing something like this:
var tmp = new String('abc');
var s = tmp.subString(0);
tmp = null;
```

### Date ([mdn](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date))
Only **using new will return the object**; Others will return the number or string.
- `new Date()`
- `new Date(2005, 0, 3)` local time; year and month is required, month is 0 index
- `Date.UTC(2005, 0, 3)` UTC time; Return number; year and month is required, month is 0 index
- Use [moment.js](http://momentjs.com/)
```js
const now = moment();
const future = moment('2030-03-30');
const diffInDays = now.diff(future, 'days');
```

### Regex
- `match`: return null or array (like)

    ```js
    const pattern = /.b(c)/
    const matches = pattern.exec('input text: abc bbc');
    matches[0] // 'abc' the whole match
    matches[1] // 'c' the 1st group
    // if with global, exec returns different mathes on multiple calls
    ```
- `test`: return boolean

### null/empty
Special objects: `null` and `undefined`
- `null`: a pointer to nothing (that's why `typeof null === 'object'`. Most case it can be replaced by `undefined`; 
- `undefined`: it's like null in other program. 
  - If you access a.name and a is {} then it returns `undefined`
  - If arr[out_of_bound_index], it returns `undefined`

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

Check string not null or empty: `!!password` (it's converted to boolean first)

Check null:
- use `typeof instance.currentPosition  !== 'undefined'` 
- Why not using `instance.currentPosition === undefined`? it can [throw error](http://stackoverflow.com/questions/4725603/variable-undefined-vs-typeof-variable-undefined) 
-  CoffeeScript:
    - coffeescript: ? or ?. (the latter can soak up so a.address?.zip returns undefined instead of typeerror)
    - CoffeeScript's existential operator `?` returns true unless a variable is `null` or `undefined`, which makes it analogous to Ruby's nil?

### comparison
- Equality operator `==`: doesn't compare type, i.e, it converts the type first (performs type coercion) then compare
    `"" == false // returns true`
- Strict Equality Operator `===`: doesn't not perform type coercion **recommended**
    `'' == false // return false`
- when comparison includes reference type, the comparison (both == and ===) performs pointer comparison.
    `{} != {}`

### Object
- the property name will always be string, even you created like this `{a:'b'}`
- `for .. in` will iterate all enumerable props (including the prototype ones) in arbitrar order
- `typeof`, check if it's a **basic type plus others**, it only returns those types: 'undefined', 'null', 'boolean', 'string', 'number', 'object', 'symbol', 'function'
    - so `typeof [] === 'object`
    - `typeof null === 'object';` See (MDN explanation)[https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/typeof]
    - usage: check method defined in prototype: `if (typeof this.sayName !== 'function')`
- `a instanceof Constructor`, check if it's a **reference type**
    - Use constructor, not string: so `[] instanceof Object`, not 'object'
- (**TODO**) Check if an object is a type
    - Why not `instanceof`?
    - Why not `typeof`? Because typeof returns only those 5 types, and array is Object type. For example, `typeof [] === 'object'`, you cannot tell if it's array. [See here](http://web.mit.edu/jwalden/www/isArray.html)
    
    ```js
    function is(type, obj) {
        var clas = Object.prototype.toString.call(obj).slice(8, -1);
        // [object String]
        return obj !== undefined && obj !== null && clas === type;
    }
    is('String', 'test'); // true
    is('String', new String('test')); // true
    ```
    
- object detection

    ```js
        // or typeof document.getElementsByName !=== 'undefined'
        if(document.getElementsByName) {
            // it means the 'getElementsByName' is supported
        }
    ```

- `JSON.stringify(obj, ['fliter', 'list])` can filter 
- [`defineProperty`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty) can set 'writable' and custom setter/getter

### Global object
Methods: 
- `isNaN, etc`
- `encodeURI()` replace space to %20
- `encodeURIComponent()` replace space and others such as '/' and '.', so don't use it for uri, only use it for uri component (thus its name)
- `let id = setTimeout(()=>console.log('future'), 1000)`, `clearTimeout(id)`
- `let id = setInterval(()=>console.log('again'), 1000)`, `clearInterval(id)`

### Function
- Always has `arguments` (note it's not `this.arguments`) for it's arguments, it's array like
- Because of 'arguments', there is no function overloading.
- Assignment makes a copy of the value only if it's a primitive type (like Number, Boolean, String, etc...). Otherwise, assignment just copies a reference to the same object (Object, Array, etc...). A new object is not created with assignment.

    ```js
    var a = {};
    var b = {name:'b'};
    var a = b;
    console.log(a.name == 'b')
    ```
- `function.length` required params length
- `Funnction.prototype.apply(scope, paramsArr)`
- `Function.prototype.call(scope, param1, param2)` the fundamental difference is that call() accepts an argument list, while apply() accepts a single array of arguments.
- Arguments are always copied **by value**. Even if the type is reference.

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
- Declaration (will be hoisted) vs Expression

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

### immediately-invoked function expression (IIFE)
- Why? It's useful when you have some work to do, some initialization maybe. You need to do it only once and you don't want to leave any globals lying around after the work is finished. 
- How? It's used to avoid hoisting and creating scope. A function creates a scope.
```js
 (function(){
   var a = 1;
   var b = 2;
   alert(a + b);
})();
```

### default value if it doesn't exist
Use ES6 default parameter instead.  
Previously: Use ||   NOTE this pattern doesn't work if the value is ''.  
```js
for timestamp, count of json["#{projectName}"]
      existing = total["#{timestamp}"] || 0
      total["#{timestamp}"] = existing + count
```




