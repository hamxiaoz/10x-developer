# DOM

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

## DOM Manipulcation

### Selector
You can use the following selector on `document` or `element`.

`const myElement = document.querySelector('#foo > div.bar input[name="login"]')`
- Returns the first descendant [`Element`](https://developer.mozilla.org/en-US/docs/Web/API/element) using DFS + Pre-order traversal
- It's not live, compare to `getElementsByTagName()`

`const myElements = document.querySelectorAll('.bar')`
- Returns [`NodeList`](https://developer.mozilla.org/en-US/docs/Web/API/NodeList)

Others: using above is recommended.
```js
const items = document.getElementsByClassName('item');
const item = document.getElementById('item');
```

### CSS
```js
// update class
myElement.classList.add('foo')
myElement.classList.remove('bar')
myElement.classList.toggle('baz')

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

### Update
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

### [Event](https://developer.mozilla.org/en-US/docs/Web/API/Event)
Don't use `onclick`: single property, essentially override it

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
