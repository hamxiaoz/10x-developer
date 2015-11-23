# CLI

## How to create a package that can be used as cli (and package)?

### Folder Structure
- use the generator: https://github.com/yeoman/generator-node
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

### Useful Libs
- interactive input https://github.com/SBoudrias/Inquirer.js
- cli helper: https://www.npmjs.com/package/meow
- full blown cli tool: https://github.com/tj/commander.js
- isolated cli, similar to REPL: https://github.com/dthree/vorpal
- shell commands, and make tool in js: https://github.com/shelljs/shelljs
    - so you can have a make file like this: https://github.com/madrobby/zepto/blob/master/make
    - to run, do `coffee make testName`
- color in cli: https://www.npmjs.com/package/chalk
![](https://github.com/chalk/ansi-styles/raw/master/screenshot.png)

A list of cli tools: https://github.com/sindresorhus/awesome-nodejs#command-line-apps