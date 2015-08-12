# JQuery
can use css style to select elements:
```js
    $('tag')
    $('.element-class')
    $('#element-id')
    $('tag[attr]') // all tag element with 'attr' attribute
    $('tag[attr*=value]') // see doc
    $('tag:first-child') // pseudo elements
    $('tag:contains('test')') // select all tag elements with text 'test'
    $('div nav a') // select all a elements in nav div.
```

constructor:
```js
    $() is a constructor to create a JQuery() object.
    $('').eq(0), get 0 index and constrcut a new jQuery object
    `$('tr').eq(0) === $($('tr')[0])`
    with context: jQuery( selector [, context ] )
```

.toggleClass('')

$(callback); is a shortcut for $(document).ready(callback).

#### What is end() and $(this)?
[ ] 
```js
    $(document).ready(function() {
       $('#faq').find('dd').hide().end().find('dt').click(function() {
         $(this).next().slideToggle();
       });
     });
```
By using end(), the first find() is undone, so we can start search with the next find() at our #faq element, instead of the dd children.
Within the click handler, the function passed to the click() method, we use $(this).next() to find the next sibling starting from the current dt. 

#### What's 'this'?
It's a context depending on caller. 
```js
     function addClickHandlers() {
       $("a.remote", this).click(function() {
         $("#target").load(this.href, addClickHandlers);
       });
     }
     $(document).ready(addClickHandlers);
```
Note the $("a.remote", this) query, this is passed as a context: For the document ready event, this refers to the document, and it therefore searches the entire document for anchors with class remote. When addClickHandlers is used as a callback for load(), this refers to a different element: In the example, the element with id target. This prevents that the click event is applied again and again to the same links, causing a crash eventually.

#### DOM:
- use val() to get value from `<input> or <textarea>` http://api.jquery.com/val/
- test() and html()

#### event:
- use on()

#### e.target vs e.currentTarget: 
if you have 'click tr', then clicking on td will trigger that event too with e.target being td and currentTarget being tr

#### get html5 data- attributes
use `attr()`. the `data()` will convert to lowercase and to camelCase. Use data() to store dynamically generated data

#### XPath
[] 
examples:
```js
    $("a[name]").css("background", "#eee" ); // add a background color to all anchor elements with a name attribute.
    $("#orderedlist > li").addClass("blue"); // This selects all child lis of the element with the id orderedlist and adds the class "blue".
```

---

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

---

# HTML

# CSS

## SASS
[SASS: differences between mixins, extends and placeholders](http://krasimirtsonev.com/blog/article/SASS-mixins-extends-and-placeholders-differences-use-cases))

# Examples
- [Form control margin](http://stackoverflow.com/questions/18562153/what-css-controls-the-right-and-left-margins-between-these-form-elements-in-twit)
- [bootstrap row click and offmenu canvas] (http://jasny.github.io/bootstrap/javascript/#fileinput)

# Bootstrap

How to use scrollspy?
- http://stackoverflow.com/questions/13134013/how-to-use-bootstrap-scroll-spy
- http://stackoverflow.com/questions/14511045/twitter-bootstrap-scrollspy-not-working-at-all
- http://stackoverflow.com/questions/12111004/how-to-activate-links-for-twitter-bootstrap-affix-component
