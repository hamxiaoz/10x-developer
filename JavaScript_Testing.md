# JavaScript Testing

## Jasmine Cheatsheet

**Spy \(for methods, can track calls or specify return value\)**

```js
// Spy on existing method
beforeEach(function() {
    foo = {
      setBar: function(value) {
        bar = value;
      }
    };

    // Spy method
    spyOn(foo, 'setBar');

    // Return specified value
    spyOn(foo, "getBar").and.returnValue(745);

    // Throw error
    spyOn(foo, "setBar").and.throwError("404");
});

// Create spy to stub method
beforeEach(function() {
    foo = {
      setBar: jasmine.createSpy('setBar')
    };

    // Test
    expect(foo.setBar).toHaveBeenCalled();
});

// Create a spy for a bare method
beforeEach(function() {
    let foo = jasmine.createSpy('foo');

    // Test
    foo('you can pass any', 'args');
    expect(foo).toHaveBeenCalledWith('you can pass any', 'args');
});
```

**Matcher**

```js
// Match with type
expect({}).toEqual(jasmine.any(Object));
expect(123).toEqual(jasmine.any(Number));

// Match function, useful to test callback function
expect(service.registerCallback).toHaveBeenCalledWith('key', jasmine.any(Function));

// Match partial object
expect(foo).toEqual(jasmine.objectContaining({
  bar: "baz",
  fooFunc: jasmine.any(Function)
}));
```

**Tips**

* Remember to call `$scope.$apply();` when testing promise. [Why?](http://davideguida.altervista.org/the-importance-of-scope-apply-when-testing-promises/)
* Call `done()` to instruct the spec is done for Asynchronous tests.

---

## Read Istanbul Report

* [http://stackoverflow.com/a/36697606](http://stackoverflow.com/a/36697606)
* [https://github.com/dwyl/learn-istanbul](https://github.com/dwyl/learn-istanbul)



