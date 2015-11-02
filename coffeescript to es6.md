# Coffeescript to ES6

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