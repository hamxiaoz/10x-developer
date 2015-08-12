# Links
- Test tool for js: https://regex101.com/

- Regex online tool for Ruby: http://rubular.com/

# Examples

#### How to replace `"name" : "basic"` to `"xxx" : "whatever you provided"`?
using grouping for everything: http://stackoverflow.com/a/6005637/166286
```csharp
// c#
string input = "'name' : 'Basic'," ;
string find = "('name'\\s:\\s')(?<text>.*)(')" ;
string replace = "$1AA$2" ;
string result = Regex.Replace (input, find, replace);
Console.WriteLine(result);
```


#### Find the number after a certain word:
```regex
(?<=%download%#)\d+
```
The lookbehind assertion (?<=foo_bar) is important because you don't want to include %download%# in your results, only the numbers after it. 
http://stackoverflow.com/questions/4740984/c-sharp-regex-matches-example 


#### Split using a maximum length (Ruby)
```
regex = /.{1,#{max_width}}/
text.scan(regex).join(zero_width_space)
```


