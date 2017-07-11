# DOM

## DOM Manipulcation

### Get
`const myElement = document.querySelector('#foo > div.bar')`
- Returns [`Element`](https://developer.mozilla.org/en-US/docs/Web/API/element)
- It's not live, compare to `getElementsByTagName()`

`const myElements = document.querySelectorAll('.bar')`
- Returns [`NodeList`](https://developer.mozilla.org/en-US/docs/Web/API/NodeList)

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

### Events
Don't use `onclick`: single property, essentially override it
