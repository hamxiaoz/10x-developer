# HTML: Form

## Hit `ENTER` to Submit Form
Form Spec:
- If a form has only one input field then hitting enter in this field triggers form submit (ngSubmit)
- if a form has 2+ input fields and no buttons or input[type=submit] then hitting enter doesn't trigger submit
  - If the form has no submit button, then the implicit submission mechanism must do nothing if the form has more than one field that blocks implicit submission.
- if a form has one or more input fields and one or more buttons or input[type=submit] then hitting enter in any of the input fields will trigger the click handler on the first button or input[type=submit] (ngClick) and a submit handler on the enclosing form (ngSubmit)

That means:
- If you only have one input, then you don't need `input[type=submit]`. Hit ENTER will submit the form.
- If you have more than one blocking input, then hitting ENTER will NOT submit the form **unless** you have a `input[type=submit]`.
  - It also means on mobile, even you see search button (because your input is type search), hitting search won't do anything. The fix is to have a hidden submit button so 'search' button works.

For Angular:
- use `ng-submit` on the form instead of `button(ng-click)` to make sure ENTER works.


## Mobile

### 'Go' or 'Search' button on Soft Keyboard
iOS:
- The 'Go' button is only shown: if the `input` tag is inside a `form` tag with `action` property. Otherwise shows a return button. See: http://stackoverflow.com/questions/22986347
- The 'Search' button is shown when `<input type='search'>` or name of the input contains 'search'

Android: 
- Shows 'Go' for text inputs
- SHows 'Next' to number inputs

### How to use keyboard 'Go' or 'Search' to submit form?
When you have submit button:
- by default the key press will submit the form

When you don't have submit button:
- if you ONLY have one input in the form, it'll work by press the 'Go'.
- if you have more than one input:
  - create a submit type button with style="visibility:hidden;position:absolute" (don't show and don't mess container layout)
Ref:
- http://stackoverflow.com/questions/5665203/getting-iphone-go-button-to-submit-form



### How to hide soft keyboard manually?
Use `blur()` on active element: https://github.com/caiogondim/hide-virtual-keyboard.js/blob/master/src/index.js 


## Library
- Address auto complete: https://developers.google.com/maps/documentation/javascript/examples/places-autocomplete-addressform
- persist form value between back: http://garlicjs.org/
