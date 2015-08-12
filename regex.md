# Links
- Test tool for js: https://regex101.com/

- Regex online tool for Ruby: http://rubular.com/

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


