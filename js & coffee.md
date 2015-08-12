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

# [Coffee](http://coffeescript.org/)

#### [coffeescript tricks](https://gist.github.com/dfurber/993584)

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

#### Check string null or empty?
`coffee: passwordNotEmpty = !!password (not empty)`

CoffeeScript's existential operator ? returns true unless a variable is null or undefined, which makes it analogous to Ruby's nil?

```js
if (variable) ... comes close, 
fails for zero, the empty string, and false. 
```

#### Add item to array?
No such function in underscore, use array function
```coffee
arr.unshift 'a'
```

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


