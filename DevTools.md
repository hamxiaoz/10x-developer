# DevTools

_ http://www.cnblogs.com/Wayou/p/chrome-console-tips-and-tricks.html

## Hotkey
Remember **all** chrome related hotkeys are trigger with `Option+CMD` or `ALT+CMD`:
- `ALT+CMD+arrow`: go to left or right tab
- `ALT+CMD+0`: go to first tab
- `ALT+CMD+9`: go to last tab
- `ALT+CMD+C`: inspect element
- `ALT+CMD+i`: open dev tools

## Elements
- `F2` to edit as HTML, press again to apply the changes.

## Network
- filter the network by using `-domain:*.com`. See full list of filters by typing `-`.
- How to capture network for new popup link? Go to [`chrome://net-internals/#events`](chrome://net-internals/#events)
- See XHRs in console: settings -> console -> check 'Log XMLHttpRequests'.

## Console
[Command Line API Reference for Chrome](https://developers.google.com/web/tools/chrome-devtools/debug/command-line/command-line-reference?hl=en)

- `$(selector)` 
    - returns the first element, is alias of `docuemnt.querySelector()`
- `$$(selector)` 
    - returns `NodeList`, is alias of `docuemnt.querySelectorAll()`
    - `NodeList` is not array, to convert to array: `Array.prototype.slice.call(div_list)` or `[...div_list]`
- `$0` is the selected element    

## Debug

Console: print and variable
- `dir(object)`
- `keys(object)`
- `table(data)`
	```js
	var names = {
		0: { firstName: "John", lastName: "Smith" },
		1: { firstName: "Jane", lastName: "Doe" }
	};
	table(names);
	```
- store as global variable `temp1`: right click on an object in the console and press “store as global variable”

Find out events:
- select element -> Event Listeners: find out existing handler for selected element.
	- for example, with unknown web app, you can find out what's happening after clicking a button.
- console: `monitor(function)` outputs when this function is called and what arguments; `unmonitor`
- console: `monitorEvents(window, "resize")`
- sources -> Event Listener Breakpoints: you can add breakpoints for all kinds of events.

	
Block	
- Blackbox: on stack, you can also blackbox the whole script.

Node
- `debugger;`
- [nif](https://github.com/thlorenz/nif)


---

## Chrome Extensions
- https://chrome.google.com/webstore/detail/builtwith-technology-prof/dapjbgnjinbpoindlpdmhochffioedbn
- https://chrome.google.com/webstore/detail/merge-windows/adjadgadeebehakpgamlnafmdkegkmph
- https://chrome.google.com/webstore/detail/web-developer-checklist/iahamcpedabephpcgkeikbclmaljebjp
- http://chrispederick.com/work/web-developer/
- http://chengyinliu.com/whatfont.html
- https://chrome.google.com/webstore/detail/emmet-review/epejoicbhllgiimigokgjdoijnpaphdp
- https://chrome.google.com/webstore/detail/onetab/chphlpgkkbolifaimnlloiipkdnihall
- postman: https://chrome.google.com/webstore/detail/postman-interceptor/aicmkgpgakddgnaphhhpliifpcfhicfo
- https://chrome.google.com/webstore/detail/dimensions/baocaagndhipibgklemoalmkljaimfdj
- feedly, evernote
