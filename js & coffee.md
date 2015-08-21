# Style

```js
$second
    .on('click',function(){ alert('hello everybody');})
    .fadeIn('slow')
    .animate({height:'120px'},500);
vs 
$second.on('click',function(){ alert('hello everybody');}).
    fadeIn('slow').
    animate({height:'120px'},500);
vs
$second.on('click',function(){ alert('hello everybody');})
    .fadeIn('slow')
    .animate({height:'120px'},500);
```

- Don't use parentheses for unary operator such as delete, void, typeof
- Prefer '' over "" for strings, from google js style guide.


# [Coffee](http://coffeescript.org/)

more coffeescript tricks: https://gist.github.com/dfurber/993584

fat arrow in coffeescript: 
- read [this](http://webapplog.com/understanding-fat-arrows-in-coffeescript/)
- use => when we need @ to be the object in which method is written; use-> when we need @ to be the object in which method is executed.

#### String with format
```coffee
print = """
  1st line
  2nd line
  #{supports interpolation}
  last line
  """
```

#### Instance method, variables
```coffee
class Songs
  _titles: 0    # instance var, Although it's directly accessible, the leading _ defines it by convention as private property.
  get_count: ->
    @_titles # access instance var
  call_another_method: ->
    return @get_count() # call another instance method
```

#### How to write function as a part of parameter
```coffee
Router.go 'home', -> 
  this.render 'home'
, 
  name: 'h'
  old: 'b'
```

### reverse for loop
coffeescript reverse for loop: `for i in [arr.length-1..0] by -1`
[iterations in coffeescript](http://discontinuously.com/2012/05/iteration-in-coffeescript/)


# [Underscore](http://underscorejs.org/)

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

#### underscore.string: https://epeli.github.io/underscore.string/

# Hows and patterns

#### value vs ref
Assignment makes a copy of the value only if it's a primitive type (like Number, Boolean, String, etc...). Otherwise, assignment just copies a reference to the same object (Object, Array, etc...). A new object is not created with assignment.
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
- `Array.prototype.reverse()` reverse the array **in place**
- how to iterate the array? don't use `for in` as it's slow

```
for(var i = 0, l = list.length; i < l; i++) {console.log(list[i]); }

// coffeescript
- array: `for item in list` or `for item, index in list`
- object: `for property, value of object` or `for own property, value of object` (use hasOwnProperty())
```

#### number
parseInt parses until found invalid character, + simply convert the string to int/float and it returns NaN if there is ANY invalid character.

#### string
- it's unicode of 16bit
- can use '+' to concatenation.
- can mix different type using '+' since JavaScript is weak typed. The non-string type is auto converted to string.
- So, if you add a string to a number (or other value) everything is converted in to a string first
```
this year is " + 2013 => "this year is 2013"
'3'+4+5 => '345'
4+5+'3' => '93'
```


#### null/empty

Special objects: `null` and `undefined`
- `null`: most case it can be replaced by `undefined`;
- `undefined`: it's like null in other program. 
  - If you access a.name and a is {} then it returns `undefined`
  - If arr[out_of_bound_index], it returns `undefined`

Check string not empty:
`coffee: passwordNotEmpty = !!password (not empty)`

Check null:
- `typeof instance.currentPosition  !== 'undefined'` http://bonsaiden.github.io/JavaScript-Garden/#types.typeof
- coffeescript: ? or ?. (the latter can soak up so a.address?.zip returns undefined instead of typeerror)
CoffeeScript's existential operator ? returns true unless a variable is null or undefined, which makes it analogous to Ruby's nil?

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

#### comparison
- Equality operator `==`: doesn't compare type, i.e, it converts the type first (performs type coercion) then compare
    `"" == false // returns true`
- Strict Equality Operator `===`: doesnt' not perform type coercion **recommended**
    `'' == false // return false`
- when comparison includes reference type, the comparison (both == and ===) performs pointer comparison.
    `{} != {}`

#### get class of object, check if an object is a type
http://bonsaiden.github.io/JavaScript-Garden/#types.typeof
check type: `Object.prototype.toString`

```js
function is(type, obj) {
    var clas = Object.prototype.toString.call(obj).slice(8, -1);
    // [object String]
    return obj !== undefined && obj !== null && clas === type;
}
is('String', 'test'); // true
is('String', new String('test')); // true
```
#### object detection
- don't add '()'
```
    if(document.getElementsByName) {
        // it means the 'getElementsByName' is supported
    }
```
- object detection is favored than browser sniffing.

#### Add item to array?
No such function in underscore, use array function
```coffee
arr.unshift 'a'
```

#### Immediate functions
All you do is add a set of parentheses after the function and this causes it to be executed right there. It's useful when you have some work to do, some initialization maybe. You need to do it only once and you don't want to leave any globals lying around after the work is finished. 
**See above (in function section) on why it has a wrapping ()**
```js
 (function(){
   var a = 1;
   var b = 2;
   alert(a + b);
})();
```

#### default value if it doesn't exist
Use ||
```js
for timestamp, count of json["#{projectName}"]
      existing = total["#{timestamp}"] || 0
      total["#{timestamp}"] = existing + count
```




