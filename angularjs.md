# AngularJS
https://github.com/jmcunningham/AngularJS-Learning

`ng-app` tells this div belongs to this angular app.

You can bind to html class attributes too!
> 
    <input type="text" ng-model="data.message">
    <div class="{{data.message}}">

#### element
All element references in Angular are always wrapped with jQuery or jqLite; they are never raw DOM references.

API: http://docs.angularjs.org/api/angular.element

How to pass parameter?
```
> <div enter="panel" leave>I'm content</div>
> app.directive("leave", function () {
  return function (scope, element, attrs) {
    element.bind("mouseleave", function () {
      element.removeClass(attrs.enter);
    });
  };
});
```

- During the linking phase, interpolation has not been evaluated yet, so if the value of a directive contains {{ }}, it is necessary to call attrs.$observe() in order to properly evaluate the value, otherwise it will return as undefined.
- They share **attri** object, which is really useful in directive (http://docs.angularjs.org/guide/directive#Attributes)

#### **Service**
Using service('name', function) or factory('name', function)?
- http://stackoverflow.com/questions/14324451/angular-service-vs-angular-factory
- http://stackoverflow.com/questions/13762228/confused-about-service-vs-factory

They are all singleton: initizlied ONLY once.
- Services: When declaring serviceName as an injectable argument you will be provided with an instance of the function. In other words new FunctionYouPassedToService().
- Factories: When declaring factoryName as an injectable argument you will be provided with the value that is returned by invoking the function reference passed to module.factory.

#### Controller
Do not use controllers for:
* Any kind of DOM manipulation — Controllers should contain only business logic. DOM manipulation—the presentation logic of an application—is well known for being hard to test. Putting any presentation logic into controllers significantly affects testability of the business logic. Angular offers databinding for automatic DOM manipulation. If you have to perform your own manual DOM manipulation, encapsulate the presentation logic in directives.
* Input formatting — Use angular form controls instead.
* Output filtering — Use angular filters instead.
* Sharing stateless or stateful code across controllers — Use angular services instead.
* Managing the life-cycle of other components (for example, to create service instances).

#### directive (http://docs.angularjs.org/guide/directive)
A directive is just a function which executes when the compiler encounters it in the DOM.

Define directive using camel cased names such as ngBind. Write directive in html by translating the camel case name into snake case with these special characters :, -, or _. 

Directive can talk to each other via other's controllers injected in link function through `require`

What's the difference between `@` and `=`?
http://stackoverflow.com/questions/14050195

#### filter
Filter should do text manipulation ONLY. If you want to add color, use directive.

Available Filters: json (convert js object to json string), limitTo (return a new array) ?? why the logic is not in controller?

#### $scope.$apply()
When and why? http://jimhoskins.com/2012/12/17/angularjs-and-apply.html
Directives Talking to Controllers, use scope.apply('method name on the scope()')


## view

#### Where to put 'view did load' init functions?
Put in controller init code. See http://stackoverflow.com/questions/16150289

