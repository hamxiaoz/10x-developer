# CLI

#### How to create a package that can be used as cli (and package)?
- use the above generator
- create a `bin` folder, create a file called: 'my-cli'
```js
#!/usr/bin/env node
require(__dirname+'/../dist/my-cli')
```
- Update your package.json:

```json
"files": [
    "dist",
    "bin"
  ],
"main": "./dist/index.js",
"bin": {
    "my-cli": "./bin/my-cli"
},

```
- To develop:
    - Write code in `lib` folder
    - Make sure the 'prepublish' script will babel your source to `dist` folder

Reference: 
- https://github.com/bevry/cson
- https://docs.npmjs.com/files/package.json
- http://javascriptplayground.com/blog/2015/03/node-command-line-tool/
- https://docs.npmjs.com/misc/scripts
