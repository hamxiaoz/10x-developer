# Angular: Mistakes I Made (MIM)

## Watch out one-way binding when bind to object
It just copies the references, so any change you made from child is actually changing the parent.

From Angular Doc and [Github Issue](https://github.com/angular/angular.js/issues/14701):
> one-way binding does not copy the value from the parent to the isolate scope, it simply sets the same value. That means if your bound value is an object, changes to its properties in the isolated scope will be reflected in the parent scope (because both reference the same object).
