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
- 
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

#### null/empty

Check string:
`coffee: passwordNotEmpty = !!password (not empty)`

Check null:
- `typeof instance.currentPosition  !== 'undefined'` http://bonsaiden.github.io/JavaScript-Garden/#types.typeof
- coffeescript: ? or ?. (the latter can soak up so a.address?.zip returns undefined instead of typeerror)
CoffeeScript's existential operator ? returns true unless a variable is null or undefined, which makes it analogous to Ruby's nil?

boolean result
```js
// the following are false on boolean expressions
false 
null
undefined
'' //the empty string
0 // the number

// true
'0' the string
[] the empty array
{} the empty object
```
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

#### How to get url of root with domain? 
`var root = location.protocol + '//' + location.host;`
http://bl.ocks.org/abernier/3070589 and http://stackoverflow.com/a/1368295/166286



