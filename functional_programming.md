# Functional Programming
WIP.

## Underscore / Lodash

Lodash Chaining:
- explicit, similar to underscore: `_.chain(numbers).map(n => n/2 === 0).value()`
- implicit, if [the result is a single value](https://lodash.com/docs#_): `_(numbers).map(n => n/2 === 0).sum()`


#### Difference between _.throttle and _.debounce?
* throttle: At most that fast, usually used when invoking source happens really frequently. Such as when typing to seach, don't send too many requests, scroll, mouse move, etc.
* debounce: wait till no change. Such as calc layout when resize is finished.

#### Convert an object into a list of \[key, value\] pairs.

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

#### \_.each cannot break out

> It's also good to note that an each loop cannot be broken out of — to break, use \_.find instead.

use `_.find` for array and `_.findKey(obj, (v, k)=>())` for object

#### How to convert a details array to a map?
This is a collection reduces to a single object. Use `reduce`.  
Borrowed from: https://github.com/rackt/react-router/blob/master/examples/sidebar/data.js

```js
const data = [
  {
    name: 'Tacos',
    description: 'A taco (/ˈtækoʊ/ or /ˈtɑːkoʊ/) is a traditional Mexican dish composed of a corn or wheat tortilla folded or rolled around a filling. A taco can be made with a variety of fillings, including beef, pork, chicken, seafood, vegetables and cheese, allowing for great versatility and variety. A taco is generally eaten without utensils and is often accompanied by garnishes such as salsa, avocado or guacamole, cilantro (coriander), tomatoes, minced meat, onions and lettuce.',
    items: [
      { name: 'Carne Asada', price: 7 },
      { name: 'Pollo', price: 6 },
      { name: 'Carnitas', price: 6 }
    ]
  },
  {
    name: 'Burgers',
    description: 'A hamburger (also called a beef burger, hamburger sandwich, burger or hamburg) is a sandwich consisting of one or more cooked patties of ground meat, usually beef, placed inside a sliced bun. Hamburgers are often served with lettuce, bacon, tomato, onion, pickles, cheese and condiments such as mustard, mayonnaise, ketchup, relish, and green chile.',
    items: [
      { name: 'Buffalo Bleu', price: 8 },
      { name: 'Bacon', price: 8 },
      { name: 'Mushroom and Swiss', price: 6 }
    ]
  },
  {
    name: 'Drinks',
    description: 'Drinks, or beverages, are liquids intended for human consumption. In addition to basic needs, beverages form part of the culture of human society. Although all beverages, including juice, soft drinks, and carbonated drinks, have some form of water in them, water itself is often not classified as a beverage, and the word beverage has been recurrently defined as not referring to water.',
    items: [
      { name: 'Lemonade', price: 3 },
      { name: 'Root Beer', price: 4 },
      { name: 'Iron Port', price: 5 }
    ]
  }
]

const dataMap = data.reduce(function (map, category) {
  category.itemsMap = category.items.reduce(function (itemsMap, item) {
    itemsMap[item.name] = item
    return itemsMap
  }, {})
  map[category.name] = category
  return map
}, {})
```

---

