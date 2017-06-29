# HTML: Form

## HTML Spec about Form Submit
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


## On Mobile
### Soft Keyboard on Input field
iOS:
- The 'Go' button is only shown, if the `input` tag is inside a `form` tag. Otherwise shows a return button. See: http://stackoverflow.com/questions/22986347
- The 'Search' button is shown when `<input type='search'>` or name of the input contains 'search'

Android: 
- Shows 'Go' for text inputs
- SHows 'Next' to number inputs
