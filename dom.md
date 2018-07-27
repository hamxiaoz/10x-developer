# DOM

- DOM = `window.document`
- BOM = `window.document, window.navigator, window.location, window.history, window.screen, etc`
- [JQuery method with native js](http://youmightnotneedjquery.com/)
- in DevTool, `$0` returns the selected Element, so you can use normal DOM APIs to access: ex, `$0.classList`

## DOM Ready

- event `DOMContentLoaded` : the browser fully loaded HTML, and the DOM tree is built, but external resources like pictures `<img>` and stylesheets may be not yet loaded.
  - `document.addEventListener("DOMContentLoaded", ready);`
  - the `defer` scripts already loaded
  - the `async` scripts might NOT be loaded
- function `load`: the browser loaded all resources (images, styles etc)
  - `window.onload = function() {}` 
- function `beforeunload/unload` : when the user is leaving the page
  - `window.unload = function() {}`

```js
// handle the case when we add the callback after the document is already loaded 
if (document.readyState === "complete" ||
    (document.readyState !== "loading" && !document.documentElement.doScroll)
) {
  callback();
} else {
  document.addEventListener("DOMContentLoaded", callback);
}
```

Reference: https://javascript.info/onload-ondomcontentloaded

Script: async vs defer
- Normally, if browser see `<script>` in `<head>`, it will stop parsing until downloaded
- script in bottom of the body will not block. But its own problem is, the script won't be downloaded until the full page is parsed.
- `defer`: async downloading scripts (download in order), execute after parsing HTML is done
- `asyc`: async downloading scripts (downloading might be out of order), execute after downloading is done (will pause parsing HTML)
- reference:
  - http://www.growingwiththeweb.com/2014/02/async-vs-defer-attributes.html
  - https://stackoverflow.com/questions/436411/where-should-i-put-script-tags-in-html-markup

## DOM Manipulcation

Node (like root Object) -> Document -> Element

### Selector
You can use the following selector on `document` or `element`.

`const myElement = document.querySelector('#foo > div.bar input[name="login"]')`
- Returns the first descendant [`Element`](https://developer.mozilla.org/en-US/docs/Web/API/element) using DFS + Pre-order traversal
- It's not live, compare to `getElementsByTagName()`

`const myElements = document.querySelectorAll('.bar')`
- Returns [`NodeList`](https://developer.mozilla.org/en-US/docs/Web/API/NodeList)
- iterate: `for .. of` or `forEach` or `.item(i)`

Compare:
- `node.contains(element)`
- `e.target.nodeName == "LI"`
- `e.target.matches('input')` (Element.matches)

Traverse:
- `element.closest('selector')`
- how to polyfill? see [MDN](https://developer.mozilla.org/en-US/docs/Web/API/Element/closest)




Others: using above is recommended.
  ```js
  const items = document.getElementsByClassName('item');
  const item = document.getElementById('item');
  ```

### Attributes

Generally, you can do:
- `element.getAttribute('id')` or `element.getAttribute('data-parent')`
- `element.setAttribute('tabindex', 3);`
- `element.id`

[Data attributes](https://developer.mozilla.org/en-US/docs/Learn/HTML/Howto/Use_data_attributes)
- js: it's accessible (read/write) from js by the `dataset` property. Note dashes are converted to camelCase)
- css: `attr()`

```js
// <article
//   id="electriccars"
//   data-columns="3"
//   data-index-number="12314"
//   data-parent="cars">
// ...
// </article>
var article = document.getElementById('electriccars');
article.dataset.columns // "3"
article.dataset.indexNumber // "12314"
article.dataset.parent = 'makes'; // "cars" -> 'makes'

// css
// article::before {
//   content: attr(data-parent);
// }
```

### CSS

On make item invisible as well as clickable: https://css-tricks.com/snippets/css/toggle-visibility-when-hiding-elements/

```js
// CRUD class
myElement.classList.add('foo', 'bar')
myElement.classList.remove('bar')
myElement.classList.toggle('baz')
myElement.classList.replace('bar', 'baz')

// fetch class
myElement.className // -> 'foo bar'
myElement.classList.contains('foo') // -> 'foo bar'

// show or hide button
stopBtn.style.display = 'none'; // '';

// set style (this won't get all styles)
myElement.style.marginLeft = '2em'

// get all styles
window.getComputedStyle(myElement).getPropertyValue('margin-left')

// Animation
const start = window.performance.now()
const duration = 2000

window.requestAnimationFrame(function fadeIn (now)) {
  const progress = now - start
  myElement.style.opacity = progress / duration

  if (progress < duration) {
    window.requestAnimationFrame(fadeIn)
  }
}
```

### Element CRUD 
```js
// create
const myNewElement = document.createElement('div')

// append
element1.appendChild(element2)

// remove
myElement.parentNode.removeChild(myElement)

// clone
const myElementClone = myElement.cloneNode()

// performant version using [DocumentFragment](https://developer.mozilla.org/en-US/docs/Web/API/DocumentFragment)
// It's minimal DOM, similar to StringBuilder
const fragment = document.createDocumentFragment()
fragment.appendChild(text)
fragment.appendChild(hr)

myElement.appendChild(fragment)

```

### Update content
```js
myElement.innerHTML = '<div>foo</div>'
myElement.textContent = 'abc'
```

## [Event](https://developer.mozilla.org/en-US/docs/Web/API/Event)
Don't use `onclick`: single property, essentially override it.

## CRUD
```js
// add
myElement.addEventListener('click', (event)=> {
  console.log(event.type + ' got fired')
})

// remove
myElement.addEventListener('change', function listener (event) {
  console.log(event.type + ' got triggered on ' + this)
  this.removeEventListener('change', listener)
})

// match all children (live too)
myForm.addEventListener('change', function (event) {
  const target = event.target
  if (target.matches('input')) {
    console.log(target.value)
  }
})
```

### Override default
- `preventDefault()` stop default handling, it'll still propagate
- `stopPropagation()` stop bubbling up
- `stopImmediatePropagation()` stop handling in current layer, stop passing to other event handlers: If several listeners are attached to the same element for the same event type, they are called in order in which they have been added. If during one such call, event.stopImmediatePropagation() is called, no remaining listeners will be called.

### e.target vs e.currentTarget:
- `e.target` identifies the element on which the event occurred
- `e.currentTarget` alawys refer to the the element to which the event handler has been attached

### `this`
- usually points to the DOM element where the handler is bound.
- NOTE if you add event using **arrow function** then it's `document` instead of the element!

### Trigger event manualy:
- https://developer.mozilla.org/en-US/docs/Web/Guide/Events/Creating_and_triggering_events

### Keyboard/Mouse events:
- See examples from: https://eloquentjavascript.net/15_event.html

### Custom events 
interface for any custom event:
- CustomEvent: https://developer.mozilla.org/en-US/docs/Web/API/CustomEvent
- custom implementation of EventEmitter

### Event Delegation
Use one event handler to handle all children events

  ```html
  <div id="menu">
    <button data-action="save">Save</button>
    <button data-action="load">Load</button>
    <button data-action="search">Search</button>
  </div>

  <script>
    class Menu {
      constructor(elem) {
        this._elem = elem;
        elem.addEventListener('click', this.onClick.bind(this)); // (*)
      }

      save() {
        alert('saving');
      }

      load() {
        alert('loading');
      }

      search() {
        alert('searching');
      }

      onClick(event) {
        let action = event.target.dataset.action;
        if (action) {
          this[action]();
        }
      };
    }

    new Menu(menu);
  </script>
  ```

Event delegation can also be used to add behavior to any element (with data-attr):

  ```js
  // use with <button data-counter>add</button>
  document.addEventListener('click', function(event) {
    if (event.target.dataset.counter != undefined) {
      // if the attribute exists...
      event.target.value++;
    }
  });
  ```
