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


# File

#### How to get the base file name: 'a.ext' -> 'a'?
```coffee
# If you know the ext name in advance:
name = path.basename filename, '.ext'

# otherwise
name = path.basename(filename).slice 0, -path.extname(filename).length
```

#### How to glob in node?
```coffee
glob = require 'glob'
dir = "d:\\Test"
glob '**/*.ext', {cwd: dir}, (error, files)->
  if error
    console.log error
    return

  _.each files, (file)->
    # file: "\\sub folder\\1.ext"
    filePath = Path.join dir, file # -> "d:\\Test\\sub folder\\1.ext"
    filename = Path.basename file # -> "1.ext"
    fileBasename = Path.basename file, '.ext' # => "1"
    
```
