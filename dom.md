# DOM

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
- defer: async downloading scripts, execute after parsing HTML is done
- asyc: async downloading scripts, execute after downloading is done (will pause parsing HTML)
- reference: http://www.growingwiththeweb.com/2014/02/async-vs-defer-attributes.html

## DOM Manipulcation

### Selector
You can use the following selector on `document` or `element`.

`const myElement = document.querySelector('#foo > div.bar input[name="login"]')`
- Returns the first descendant [`Element`](https://developer.mozilla.org/en-US/docs/Web/API/element) using DFS + Pre-order traversal
- It's not live, compare to `getElementsByTagName()`

`const myElements = document.querySelectorAll('.bar')`
- Returns [`NodeList`](https://developer.mozilla.org/en-US/docs/Web/API/NodeList)
- `for .. of` or `forEach`

Check element:
- `e.target.nodeName == "LI"`
- `e.target.matches('input')`

Others: using above is recommended.
```js
const items = document.getElementsByClassName('item');
const item = document.getElementById('item');
```

### Attributes

id:

```js
// id
const element = document.querySelector('#app').id;
element.id;
```

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

### CRUD
```js
// create
const myNewElement = document.createElement('div')

// remove
myElement.parentNode.removeChild(myElement)


// clone
const myElementClone = myElement.cloneNode()

// append
element1.appendChild(element2)

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

override:
- `preventDefault()` stop default handling, it'll still propagate
- `stopPropagation()` stop bubbling up
- `stopImmediatePropagation()` stop handling in current layer, stop passing to other event handlers: If several listeners are attached to the same element for the same event type, they are called in order in which they have been added. If during one such call, event.stopImmediatePropagation() is called, no remaining listeners will be called.

e.target vs e.currentTarget:
- `e.target` identifies the element on which the event occurred
- `e.currentTarget` alawys refer to the the element to which the event handler has been attached

`this`:
- usually points to the DOM element where the handler is bound.
- NOTE if you add event using **arrow function** then it's `document` instead of the element!

### Keyboard/Mouse events
See examples from: https://eloquentjavascript.net/15_event.html
