# RegEx

## Links

* Test tool for js: [https://regex101.com/\#javascript](https://regex101.com/#javascript)
* For Ruby: [http://rubular.com/](http://rubular.com/)
* Debug regex: [https://www.debuggex.com/](https://www.debuggex.com/)
* Cheat Sheet: [http://www.cheatography.com/davechild/cheat-sheets/regular-expressions/pdf/](http://www.cheatography.com/davechild/cheat-sheets/regular-expressions/pdf/)

## Usage

See [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/String/search](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/search)

```javascript
'str'.search(/pattern/) // returns index
/pattern/.test('str') // : boolean
/pattern/.exec('str') // return null or matches array ([0] is full string, [1].. is group
```

## Checklist

* Be careful about the greedy matching `.*`,  try to add `?` to use lazy matching: `.*?`. See [here](https://blog.mariusschulz.com/2014/06/03/why-using-in-regular-expressions-is-almost-never-what-you-actually-want)
* Positive lookahead \(does incldue\): `(?=...)`
* Negative lookahead \(not include multiple chars\): `(?!...)`
  * to match a single char that's not in the list, you can use `[^abc]` \(means match one char that's not a or b or c\)
* Positive lookbehind: `(?<=...)` **NOTE JavaScript doens't have this**. You can use negative lookahead

## Examples

### How to replace `"name" : "basic"` to `"xxx" : "whatever you provided"`?

using grouping for everything: [http://stackoverflow.com/a/6005637/166286](http://stackoverflow.com/a/6005637/166286)

```csharp
// c#
string input = "'name' : 'Basic'," ;
string find = "('name'\\s:\\s')(?<text>.*)(')" ;
string replace = "$1AA$2" ;
string result = Regex.Replace (input, find, replace);
Console.WriteLine(result);
```

### Find the number after a certain word:

```text
(?<=%download%#)\d+
```

The lookbehind assertion \(?&lt;=foo\_bar\) is important because you don't want to include %download%\# in your results, only the numbers after it.  
[http://stackoverflow.com/questions/4740984/c-sharp-regex-matches-example](http://stackoverflow.com/questions/4740984/c-sharp-regex-matches-example)

### How to make sure string 'po box' is not in the test string:

Use negative lookahead: `/^(?!.*po\sBOX).*$/`

### How to find a pattern before a word:

Let's say we want to match and replace `:user` in the url `abc.com/:user/notebooks/:user-name/:userName`  
Use We could use: `/:user(?=\b)/`, which will match the first `:user` and `:user-name` but not `:userName`.

### Split using a maximum length \(Ruby\)

```text
regex = /.{1,#{max_width}}/
text.scan(regex).join(zero_width_space)
```

### Match string insdie single quotes

[https://regex101.com/r/uH6uK3/1](https://regex101.com/r/uH6uK3/1)

```javascript
var result = [];
const pattern = /'([^',]+)'/g;
var match;
while(match = pattern.exec("'a','b', 'c'")) {
    result.push(match[1]);
}
console.log(result);
```

### match a word

* use word boundary: \b
* be sure to be lazy \(+?\)

```javascript
const re = /^\/(.+?)\b/;
re.exec('/abc/def')[1] // -> abc
re.exec('/abc-def')[1] // -> abc
re.exec('/abc_def')[1] // -> abc_def
```

