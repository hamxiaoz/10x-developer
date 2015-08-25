# HTML

#### Basics
- file protocol has three forward slashes: `file:///`
- Use <q> to mean quotes. It makes the content more structural than double quotes '"' as not in all language that the double quotes is used for quoting.
- Use <blockquote> to quote a block of text. The default browser behavior is to indent the text block.
- 对于 HTML，您无法通过在 HTML 代码中添加额外的空格或换行来改变输出的效果。当显示页面时，浏览器会移除源代码中多余的空格和空行。所有连续的空格或空行都会被算作一个空格。
- `ul` `li` are block items
  - how to use custom marker for bullet points? `list-style-image: url(image/backpack.gif)`
- basic HTML5 structure
```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="utf-8">
    </head>
    <body>
    </body>
</html>
```

URL Query String: ` http://server/path/program?query_string`

Charater entity: 
- &gt, &lt, &amp, &copy, or use &#100 (use number instead of names)
- http://www.w3schools.com/tags/ref_entities.asp
- JavaScript provides functions `encodeURIComponent` and `decodeURIComponent` to add these codes to strings and remove them again

img
- Jpeg:lossy information format
- Png: lossless format
- Gif: up t 256 colors. Only one color can be set to transparent.
- always provide alternative `<img src="x“ alt="this should be the picture content" >`
- <img> is a inline element. So if you have multiple images, they will be put side by side by default.
- you can use css to always add a background image to any element:
```css
    background-image: url(images/background.gif);
    background-repeat: no-repeat;
    background-position: top left;
```

table
- table cel has no margin property. Use border-spacing from table to specify the entire table.
- use rowspan to span cell across rows. The spanned row therefore doesn't need to have the td cells.
- DON'T use table to layout stuff! Think about my gift page, do I need to use table to layout? I think it's fine for table as they are tabular data. (p607)
    - table in html tells your data is in the relationships of tabular data items. In general, table is not used for presentation.
    - table in css gives you a way to display block-level elements. If you just want to use a table-like presentation, then use css table.
    - table cannot be loaded faster, the whole thing has to be loaded for browser to determine layout. It cannot be easily cached either.
- You can also use `dl` to display key/value pair, like table

table css:
```
div.tableRow { display: table-row; }
div.tableRow p { display: cell; }
```
css table, when you use it, make sure you add the following to the cell div, otherwise the cell content is aligned to middle or bottom! (p520)
    vertical-align: top;



<lable> use label and property 'for' with id: `<label for="id of the lable points to">text</label>`

#### form
- radio has same name
```html
<form>
<input type="radio" name="sex" value="male" checked>Male
<br>
<input type="radio" name="sex" value="female">Female
</form> 
```
- select, name, option, value (select can have a `multiple` boolean attribute)
```html
<select name="cars">
  <option value="volvo">Volvo</option>
  <option value="saab">Saab</option>
  <option value="opel">Opel</option>
  <option value="audi">Audi</option>
</select>
```
- use 'required' boolean property to make sure the field is not empty when submitting.
- How to style file input? [Wrap it under label and hide it](http://stackoverflow.com/a/25825731/166286)
```html
<label class="custom-file-upload">
    <input type="file"/>
    Custom Upload
</label>
```
- how to access elements of a form?
```html
<form name="myForm">  
    <input type="text" name="foo" id="foo" />
```
```js
document.getElementById('foo'); // preferred
document.getElementById("myform").elements["foo"];
document.myForm.foo; // note it might return foo property of the form instead of foo element.
// http://stackoverflow.com/questions/2435525/best-practice-access-form-elements-by-html-id-or-name-attribute
```


`<abbr>` use it instead of `<acronym>`, abbreviation is not a word (DOM is acronym).
```html
<p>I do <abbr title="Hypertext Markup Language">HTML</abbr></p>
```


<video> tag: 
- they are boolean attributes such as 'controls'
- video = container (mp4/webm/ogg/flash) + video(encoded with H.264/VP8) + audio(encoded with AAC/Vorbis)
```html
    <video controls autoplay width="515" height="234" poster="image that displays when video is not playing">
        <source src="sd/dsfsd.mp4">
        <source src="sd/dsfsd.webm" type='video/ogg; codecs="theora, vorbis"'> <!-- NOTE use single quote to wrap double quotes -->
        <object>this should be the fallback flash player</object>
        <p>the text is displayed if your video is NOT supported</p>
    </video>
```

---

# DOM

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
    - `$('#checkbox').prop('checked')`
    - `$('#checkbox').is(':checked')`
    - select `$('#checkbox').filter(':checked')`
    - `$('#input[type="checkbox"]:checked')`
    - `$('#input[type="checkbox"]:not(:checked)')`

- how to check: (it doesn't trigger event by default, use change() to trigger change event)
`$('.myCheckbox').prop('checked', true)`

- how to disable:
```coffee
if disable
    $('input[type="checkbox"]:not(:checked)').attr 'disabled', true
else
    $('input[type="checkbox"]:not(:checked)').removeAttr 'disabled'
```


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

#### What is `end()`?

Use [.end()](http://api.jquery.com/end/) to pop up stack: end the most recent filtering operation in the current chain and return the set of matched elements to its previous state.
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

#### Console & Debug

`debugger;`

If the result is 0, the elements are not in the DOM:
 `console.log($(".theElements").length);`
 
_ Debug JQuery: http://fixingthesejquery.com/#slide23

