JavaScript Event Loop and Others
================================

![](https://cdn-images-1.medium.com/max/800/1*4lHHyfEhVB0LnQ3HlhSs8g.png)

Runtime = Web APIs (DOM + setTimeout + fetch, etc) + Event Loop + Callback Queue + V8

The JavaScript Engine (V8) = Memory Heap + Call Stack + JIT

- JavaScript is single thread
- The runtim provides event loop
- Single Thread: single thread of execution.
- Almost all I/O is non-blocking. HTTP, db, file
- Web Worker: it's a separate message queue + event loop + memory

Event Loop: monitor 'Call Stack' + 'Callback Queue'/'Message queue'
- it runs the function from 'Call Stack'
- each entry is called 'Call Frame'
- runtime execute async operation and put callback into 'Callback Queue'
- only when 'Call Stack' is empty, it takes the first event from 'Callback Queue'
  - that's why even you do setTimeout(func, 0) it'll still wait till current execution is done then pulling the func from queue

example: event
- when user click a button, and let's say there is a callback function on 'click', then what happens is: the event + callback is added to 'message queue'
- event loop monitor the queue, if dequeue the above item, the callback function is called
- only when the above callback function is done, event loop continues

## setTimeout
setTimeout: only garuantee how long is the timer (once done add callback to queue)
- itself doesn't add the callback to queue, it only setup the timer, when timer finishes, then rumtime addes the callback function to the queue.
- but if queue has other callback, even you do setTimeout(fn, 0) it won't be executed immediately
- the delay time means: when the runtime put the callback to the queue. As for when the callback is executed, that'll depends on current call stack (it has to be empty) as well as current queue (first in first out)
- Timers can be nested; after five such nested timers, however, the interval is forced to be at least 4 milliseconds.

```js
console.log('a');
setTimeout(() => console.log('b'), 0)
console.log('c');
// output: a, c, b
```


setTimeout vs setInterval
- https://javascript.info/settimeout-setinterval
- setTimeout will guarantees a fixed deplay from each functions