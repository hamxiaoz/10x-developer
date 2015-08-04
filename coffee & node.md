#### String with format
```coffee
print = """
  1st line
  2nd line
  #{supports interpolation}
  last line
  """
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
    
```
