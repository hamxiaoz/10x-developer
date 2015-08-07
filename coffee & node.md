# [Coffee](http://coffeescript.org/)

#### String with format
```coffee
print = """
  1st line
  2nd line
  #{supports interpolation}
  last line
  """
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
