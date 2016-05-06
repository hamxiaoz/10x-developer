# Node.js

## Guide
http://stackoverflow.com/questions/2878008/how-do-i-create-a-non-blocking-asynchronous-function-in-node-js
> It's important to understand that node isn't about functions being asynchronous all the time. It's about i/o being asynchronous and non-blocking. If your function doesn't do any i/o, node isn't going to help you make it asynchronous. It provides tools that will allow you to do that though. Like child processes. That's what felix's answer is getting at. Your function can spawn a child process to do your work and it will execute off of the main event loop.

## Node Package

### How to use local (private) package?
Use git submodule

```bash
# when clone, remember to clone with submodules
git clone --recursive git@REPO-URL

# to update
git submodule update --remote
npm install
```

NOTE there is a bug for `npm update`: it doesn't work with local package now, see [NPM #7426](https://github.com/npm/npm/issues/7426)
```js
"my-package": "file:./my-package",
```
So my workaroud for now is, go to node_moduels folder and delete the package folder, then npm install again.


Reference:
- http://stackoverflow.com/a/17371987/166286

### File

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

---

## Frontend

#### How to get url of root with domain? 
`var root = location.protocol + '//' + location.host;`
http://bl.ocks.org/abernier/3070589 and http://stackoverflow.com/a/1368295/166286

#### A way to generate and download CSV files client-side
https://gist.github.com/hamxiaoz/a664f52e34c22f2be83f



