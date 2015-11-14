## JSON Style Guide
Ref: 
- https://google.github.io/styleguide/jsoncstyleguide.xml

Highlights:
- No comments
- All property names must be surrounded by double quotes
- Property names must be camel-cased, ascii strings.

---

## [Underscore](http://underscorejs.org/) and [underscore.string](https://epeli.github.io/underscore.string/)

#### Difference between _.throttle and _.debounce?
At most that fast vs wait till no change https://ruby-china.org/topics/22494

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

### Type: value/ref
- String is value type
- ref type: function, object, array
- Assignment makes a copy of the value only if it's a primitive type (like Number, Boolean, String, etc...). Otherwise, assignment just copies a reference to the same object (Object, Array, etc...). A new object is not created with assignment.
```js
    var a = {};
    var b = {name:'b'};
    var a = b;
    console.log(a.name == 'b')
```

#### Array
```js
var a = Array(4); // []
var a = Array('4'); // returns [4]
var a = Array()
var a = Array('a', 'b');
var a = ['a', 'b']
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
- **in place** copy itself to itself, [start, end) not including the endIndex: `copyWithin(targetIndex, startIndex, endIndex)`
- Reverse **in place**:   `Array.prototype.reverse()` 
- Concat
    - return new array: `arr.concat(arr2)`
    - **in place (append b to a)**: `Array.prototype.push.apply(a,b)`
- Add item to head: `arr.unshift('a')`
- how to iterate the array? `for(let i = 0, l = list.length; i < l; i++) {console.log(list[i]); }`
- Test all: `_.all` or `_.every` or `arr.every((element) => true)`

### number
- `parseInt` parses until found invalid character, + simply convert the string to int/float and it returns NaN if there is ANY invalid character.
- always use radix: `parseInt('09', 10)` Otherwise '09' will be treated as hex and result as 0

### string
- it's unicode of 16bit
- can use '+' to concatenation.
- can mix different type using '+' since JavaScript is weak typed. The non-string type is auto converted to string.
- So, if you add a string to a number (or other value) everything is converted in to a string first
```
this year is " + 2013 => "this year is 2013"
'3'+4+5 => '345'
4+5+'3' => '93'
```


### null/empty
Special objects: `null` and `undefined`
- `null`: most case it can be replaced by `undefined`; NOTE `typeof null // 'object'`
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
NaN

// Anything except the above is true, for example:
'0' // the string
[] // the empty array
{} // the empty object
```

(**TODO**) Check string not empty: `!!password` (it's converted to boolean first)

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
- (**TODO**) Check if an object is a type
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

- `JSON.stringify(obj, ['fliter', 'list])`

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




