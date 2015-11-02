# Coffeescript to ES6 Cheatsheet

References:
- https://gist.github.com/danielgtaylor/0b60c2ed1f069f118562
- https://robots.thoughtbot.com/replace-coffeescript-with-es6

## Iteration

- On object properties:

```js
// coffee
for prop, value of obj

// ES6
_.each(obj, (value, key)=>{
});
```

- On collection (array):

```js
// coffee
for ele in arr
    console.log ele
    
// es6
for (let ele of arr) {
    console.log(ele);
}

// or
arr.forEach( (ele) => {
    console.log(ele);
    //  函数体内的this对象，就是定义时所在的对象，而不是使用时所在的对象
});

// or
arr.forEach(function(ele){
    console.log(ele);
    //  this is the function
});
```