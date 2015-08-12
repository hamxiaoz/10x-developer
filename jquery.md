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
