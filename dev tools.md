# Dev Tools

[Command Line API Reference for Chrome](https://developers.google.com/web/tools/chrome-devtools/debug/command-line/command-line-reference?hl=en)

- `$(selector)` 
    - returns the first element, is alias of `docuemnt.querySelector()`
- `$$(selector)` 
    - returns `NodeList`, is alias of `docuemnt.querySelectorAll()`
    - `NodeList` is not array, to convert to array: `Array.prototype.slice.call(div_list)` or `[...div_list]`