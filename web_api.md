# Web APIs

## HTTP

Fetch: https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch

* a better version of XHR
* it returns Promise: `fetch(`https://api.github.com/users/${this.name}`) .then(resp => resp.json());`
* 4xx and 5xx are not considerd as error so it's in then
* living standard: safari and IE not support it

```js
// GET
fetch('./api/some.json')
  .then(
    function(response) {
      if (response.status !== 200) {
        console.log('Looks like there was a problem. Status Code: ' +
          response.status);
        return;
      }

      // Examine the text in the response
      response.json().then(function(data) {
        console.log(data);
      });
    }
  )
  .catch(function(err) {
    console.log('Fetch Error :-S', err);
  });

// POST with form data, multipart/form-data
// More: https://stackoverflow.com/questions/46640024
let formData = new FormData();
formData.append('name', 'John');
formData.append('password', 'John123');

fetch("api/SampleData", {
  body: formData,
  method: "post"
});
```

XMLHttpRequest:

  ```js
  // JSON
  var req = new XMLHttpRequest();
  req.responseType = 'json';
  req.open('GET', url, true);
  req.onload  = function() {
    var jsonResponse = req.response;
    // do something with jsonResponse
  };
  req.send(null);


  // JSON
  function reqListener() {
    var data = JSON.parse(this.responseText);
    console.log(data);
  }
  function reqError(err) {
    console.log('Fetch Error :-S', err);
  }
  var oReq = new XMLHttpRequest();
  oReq.onload = reqListener;
  oReq.onerror = reqError;
  oReq.open('get', './api/some.json', true);
  oReq.send();
  ```



## Web Workers
- background thread (other than UI thread)
- cannot access DOM
- different context window

## Sevice Worker
- Proxy between browser and network. Handles network requests. Thus enabling offline experience.
- it's web worker and more
- cannot access DOM

## Web Socket
Communicate from browser to server.

- Socket.IO: A long polling/WebSocket based third party transfer protocol for Node.js.


## MutationObserver
The MutationObserver interface provides the ability to watch for changes being made to the DOM tree.