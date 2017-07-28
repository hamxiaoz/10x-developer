# DOM

## DOM Manipulcation

### Selector
`const myElement = document.querySelector('#foo > div.bar')`
- Returns [`Element`](https://developer.mozilla.org/en-US/docs/Web/API/element)
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
