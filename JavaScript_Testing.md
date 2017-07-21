# JavaScript Testing

- [Jasmine Cheatsheet](#jasmine-cheatsheet)

---

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

// Use spy to stub a method
beforeEach(function() {
    foo = {
      setBar: jasmine.createSpy('setBar')
    };

    // Test
    expect(foo.setBar).toHaveBeenCalled();
});

// Use spy to create bare method
beforeEach(function() {
    let foo = jasmine.createSpy('foo');

    // Test
    foo('you can pass any', 'args');
    expect(foo).toHaveBeenCalledWith('you can pass any', 'args');
});

// Use spy to create an object containing multiple methods
// Useful for mocking Angular service
beforeEach(function() {
    let $window = jasmine.createSpyObj<angular.IWindowService>('$window', ['open', 'alert']);
    (<jasmine.Spy>$window.alert).and.returnValue({});

    // Test
    $window.open();
    expect($window.open).toHaveBeenCalled();
});

// Use spy to create an object containing both methods and property
// You cannot use createSpyObj as it's for methods only
beforeEach(function() {
    foo = {
      bar: {},
      setBar: jasmine.createSpy('setBar')
    };

    // Test
    foo.setBar();
    expect(foo.bar).toEqual({});
    expect(foo.setBar).toHaveBeenCalled();
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
* Call the following methods when you testing $httpBackend. See [doc](https://docs.angularjs.org/api/ngMock/service/$httpBackend) and [source code](https://github.com/angular/angular.js/blob/master/src/ngMock/angular-mocks.js#L1860)

    ```typescript
    afterEach(()=> {
      $httpBackend.verifyNoOutstandingRequest();
      (<any>$httpBackend).verifyNoOutstandingExpectation(false);
    });
    ```

## Jasmine + Angular

Test component:

```js
describe('My Tests', () => {
  let $scope: angular.IScope,
    $q: angular.IQService
    $componentController: angular.IComponentControllerService;

  beforeEach(() => {
    angular.mock.module('module name');

    inject(($injector : angular.auto.IInjectorService)=> {
      $scope = $injector.get<angular.IRootScopeService>('$rootScope');
      $q = $injector.get<angular.IQService>('$q');
      $componentController = $injector.get<angular.IComponentControllerService>('$componentController');
    });
  });

  it('should skip', () => {
    pending();
  });
});
```

Test Service itself: mock http

```ts
import {MyService} from './my-service';

import IHttpService = angular.IHttpService;
//import IQService = angular.IQService;
import IHttpBackendService = angular.IHttpBackendService;
//import IRootScopeService = angular.IRootScopeService;

describe('My Service', ()=> {

  let myService: MyService,
      $http: IHttpService,
      $httpBackend: IHttpBackendService,
      $q: IQService,
      $rootScope: IRootScopeService;

  beforeEach(()=> {
    angular.mock.module('myModule');

    inject(($injector: angular.auto.IInjectorService)=> {
      $q = $injector.get<angular.IQService>('$q');
      $http = $injector.get<angular.IHttpService>('$http');
      $httpBackend = $injector.get<angular.IHttpBackendService>('$httpBackend');
      $rootScope = $injector.get<angular.IRootScopeService>('$rootScope');
    });

    myService = new MyService($http);
  });

  it('Should make HTTP call', (done)=> {
    $httpBackend.expectGET(`/URL/URL`).respond(200, 'fake data');

    myService.getData()
      .then(done);
    $httpBackend.flush();
  });
});
```

Test service in component:

```ts
let myService = jasmine.createSpyObj('myService', ['getData']);
(<jasmine.Spy>myService.getData).and.returnValue($q.when({}));
```

Mistakes to avoid:
- Always to remember to return a promise!
- In test, always do a $scope.$digest() after calling a promise so that it triggers the promise chain.

---

## Read Istanbul Report

* [http://stackoverflow.com/a/36697606](http://stackoverflow.com/a/36697606)
* [https://github.com/dwyl/learn-istanbul](https://github.com/dwyl/learn-istanbul)



