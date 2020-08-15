# CLI command line tool

## How to create a package that can be used as cli \(and package\)?

### Folder Structure

* use the generator: [https://github.com/yeoman/generator-node](https://github.com/yeoman/generator-node)
* create a `bin` folder, create a file called: 'my-cli'

  ```javascript
  #!/usr/bin/env node
  require(__dirname+'/../dist/my-cli')
  ```

* Update your package.json:

```javascript
"files": [
    "dist",
    "bin"
  ],
"main": "./dist/index.js",
"bin": {
    "my-cli": "./bin/my-cli"
},
```

* So the flow is:
  * We tell package the bin file is in the `bin` folder
  * The bin file invokes the actual script in `dist` folder
  * We develop the script in `lib` folder and babel the source \('prepublish'\) to `dist` folder
  * To test locally on dev machine

    ```bash
    npm link
    # then start using the cli version
    ```

  * To publish internally, do

    ```bash
    npm version minor # update version
    npm pack # this will create the abc-1.0.0.tgz file

    # to install and use
    npm install -g abc-1.0.0.tgz
    ```

Reference:

* [https://github.com/bevry/cson](https://github.com/bevry/cson)
* [https://docs.npmjs.com/files/package.json](https://docs.npmjs.com/files/package.json)
* [http://javascriptplayground.com/blog/2015/03/node-command-line-tool/](http://javascriptplayground.com/blog/2015/03/node-command-line-tool/)
* [https://docs.npmjs.com/misc/scripts](https://docs.npmjs.com/misc/scripts)

### Useful Libs

* interactive input [https://github.com/SBoudrias/Inquirer.js](https://github.com/SBoudrias/Inquirer.js)
* cli helper: [https://www.npmjs.com/package/meow](https://www.npmjs.com/package/meow)
* full blown cli tool: [https://github.com/tj/commander.js](https://github.com/tj/commander.js)
* isolated cli, similar to REPL: [https://github.com/dthree/vorpal](https://github.com/dthree/vorpal)
* shell commands, and make tool in js: [https://github.com/shelljs/shelljs](https://github.com/shelljs/shelljs)
  * so you can have a make file like this: [https://github.com/madrobby/zepto/blob/master/make](https://github.com/madrobby/zepto/blob/master/make)
  * to run, do `coffee make testName`
* color in cli: [https://www.npmjs.com/package/chalk](https://www.npmjs.com/package/chalk)

  ![](https://github.com/chalk/ansi-styles/raw/master/screenshot.png)

A list of cli tools: [https://github.com/sindresorhus/awesome-nodejs\#command-line-apps](https://github.com/sindresorhus/awesome-nodejs#command-line-apps)

