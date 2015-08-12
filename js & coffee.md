# Style

```js
$second
    .on('click',function(){ alert('hello everybody');})
    .fadeIn('slow')
    .animate({height:'120px'},500);
vs 
$second.on('click',function(){ alert('hello everybody');}).
    fadeIn('slow').
    animate({height:'120px'},500);
vs
$second.on('click',function(){ alert('hello everybody');})
    .fadeIn('slow')
    .animate({height:'120px'},500);
```

- Don't use parentheses for unary operator such as delete, void, typeof
- Prefer '' over "" for strings, from google js style guide.


# [Coffee](http://coffeescript.org/)

more coffeescript tricks: https://gist.github.com/dfurber/993584

fat arrow in coffeescript: 
- read [this](http://webapplog.com/understanding-fat-arrows-in-coffeescript/)
- use => when we need @ to be the object in which method is written; use-> when we need @ to be the object in which method is executed.
- 
#### String with format
```coffee
print = """
  1st line
  2nd line
  #{supports interpolation}
  last line
  """
```

#### Instance method, variables
```coffee
class Songs
  _titles: 0    # instance var, Although it's directly accessible, the leading _ defines it by convention as private property.
  get_count: ->
    @_titles # access instance var
  call_another_method: ->
    return @get_count() # call another instance method
```

#### How to write function as a part of parameter
```coffee
Router.go 'home', -> 
  this.render 'home'
, 
  name: 'h'
  old: 'b'
```

### reverse for loop
coffeescript reverse for loop: `for i in [arr.length-1..0] by -1`
[iterations in coffeescript](http://discontinuously.com/2012/05/iteration-in-coffeescript/)


# [Underscore](http://underscorejs.org/)

#### Difference between _.throttle and _.debounce?
At most that fast vs wait till no change https://ruby-china.org/topics/22494

#### Convert an object into a list of [key, value] pairs.
```js
_.pairs({one: 1, two: 2, three: 3});
=> [["one", 1], ["two", 2], ["three", 3]]
```

#### how to union with array?
```coffee
a = [1, 2]
b = [3, 4, 5]
c = [6]

console.log _.union(a, b, c)

arr = [a, b, c]
console.log _.union.apply(_, arr)
```

#### underscore.string: https://epeli.github.io/underscore.string/

# Hows and patterns

#### null/empty

Check string:
`coffee: passwordNotEmpty = !!password (not empty)`

Check null:
- `typeof instance.currentPosition  !== 'undefined'` http://bonsaiden.github.io/JavaScript-Garden/#types.typeof
- coffeescript: ? or ?. (the latter can soak up so a.address?.zip returns undefined instead of typeerror)
CoffeeScript's existential operator ? returns true unless a variable is null or undefined, which makes it analogous to Ruby's nil?

boolean result
```js
// the following are false on boolean expressions
false 
null
undefined
'' //the empty string
0 // the number

// true
'0' the string
[] the empty array
{} the empty object
```
#### get class of object, check if an object is a type
http://bonsaiden.github.io/JavaScript-Garden/#types.typeof
check type: `Object.prototype.toString`

```js
function is(type, obj) {
    var clas = Object.prototype.toString.call(obj).slice(8, -1);
    // [object String]
    return obj !== undefined && obj !== null && clas === type;
}
is('String', 'test'); // true
is('String', new String('test')); // true
```
#### object detection
- don't add '()'
```
    if(document.getElementsByName) {
        // it means the 'getElementsByName' is supported
    }
```
- object detection is favored than browser sniffing.

#### Add item to array?
No such function in underscore, use array function
```coffee
arr.unshift 'a'
```

#### Immediate functions
All you do is add a set of parentheses after the function and this causes it to be executed right there. It's useful when you have some work to do, some initialization maybe. You need to do it only once and you don't want to leave any globals lying around after the work is finished. 
**See above (in function section) on why it has a wrapping ()**
```js
 (function(){
   var a = 1;
   var b = 2;
   alert(a + b);
})();
```

#### default value if it doesn't exist
Use ||
```js
for timestamp, count of json["#{projectName}"]
      existing = total["#{timestamp}"] || 0
      total["#{timestamp}"] = existing + count
```

#### How to get url of root with domain? 
`var root = location.protocol + '//' + location.host;`
http://bl.ocks.org/abernier/3070589 and http://stackoverflow.com/a/1368295/166286


# DOM Related

Concept/Thinking
- progressive enhancement: make your core content first, don't add important content using JavaScript (search engine can't search)
- graceful degration
- don't use '#'?

DOM
- you can use element.src = 'ss' to replace element.setAttribute('src', 'ss'), **but it's old method and not DOM**. Stick with DOM API!
- don't use psuedo-protocal like this:
    `<a href="#" onclick="javascript:window.open();">example</a>`
- don't use document.write()
- use element.innerHTML wisely, as it's replacing the whole value inside the element. (no fine-grain control,

```
DOM CORE
    pic.getAttribute("src")
    document.getElementsByTagName("body").firstChild
HTML-DOM
    pic.src
    document.body
```



event
- eventName = "JavaScript Statement1; statement2;"
- 'this' means the invoking element.
- return false to prevent default behavior.
- don't use inline javascript to add event:
    `<a onlick="javascript code">`
- don't use 'onclick', it's the same as inline, and the event becomes a property, which can be overritten.
- use 'addEventListener' or 'attachevent', better yet, use JQuery.
```
    $('#id').on("click", function(event){alert($(this).text()); }); // JQeury
    element.addEvent(type, fn); // MooTools
```

#### input
- `input` (keyevents) and `change` (user has commmited, like blur) 
- http://www.w3.org/TR/html5/forms.html#event-input-input]
- get input content: `$().val()`
- trigger change event on input/textarea/select: `$( ".target" ).change()` or `$( ".target" ).trigger('change')`

#### checkbox:
- how to check if it's checked: 
`$('#checkbox').prop('checked')` or `$('#checkbox').is(':checked')` or select `$('#checkbox').filter(':checked')`
or `$('#input[type="checkbox"]:checked')`

- how to check: (it doesn't trigger event by default, use change() to trigger change event)
`$('.myCheckbox').prop('checked', true)`


getElementsByTagName can also work on the element:
```
    var table = document.getElementById("forecast-table"); 
    var cells = table.getElementsByTagName("td");
```

childNodes
```
    var p = document.getElementById("testText"); // it's a p element
    // p.nodeValue is null, the text is its first child's value
    var text = p.childNodes[0].nodeValue;
```
- firstChild is the same as childNodes[0]

- nodeValue: text of the node if textNode.
- nodeType:
  - element node (1)
  - attribute node (2)
  - text node (3)

- className: set/get class for the html element.
- createElement: create <p>
- createTextNode: create text for <p>
- appendChild
```
    <p>This is <em>my<em> content</p>
                ||
    text node(This is) + element node(em) + text node(content)
                            |
                        text node(my)
```
- insertBefore
    `targetElement.parentNode.insertBefore(newElement, targetElement)`
- why do we need parent node? Think about the function is telling the parent node to insert an element inside it.

insertAfter (custom function)
```
    function insertAfter(newElement, targetElement) {
        var parent = targetElement.parentNode;
        if(parent.lastChild == targetElement) {
            parent.appendChild(newElement);
        } else {
            parent.insertBefore(newElement, targetElement.nextSibling);
        }
    }
```

lastChild:
- **don't assume the node is always an elment node**. For example, some browser might add a 'line break' text node:
```
        <blockquote>
            sdfsdfdfsf <br>
            2nd line <br>
            this is <abbr title="abbriation">abbr</abbr>
        </blockquote>
```
last child for blockquote is the line break.

in this case, to get the last element (not the node), use this:
    element.getElementsByTagName("*")[element.getElementsByTagName("*").length-1]

css related:
- '-' is reserved keyword, so 'background-color' is illegal. Use cameralCase: backgroundColor.
- use element.style **only** works if the style is directly set in html.
