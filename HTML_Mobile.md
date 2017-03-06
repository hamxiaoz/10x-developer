## Form

### Soft Keyboard on Input field
iOS:
- The 'Go' button is only shown, if the `input` tag is inside a `form` tag. Otherwise shows a return button. See: http://stackoverflow.com/questions/22986347
- The 'Search' button is shown when `<input type='search'>` or name of the input contains 'search'

Android: 
- Shows 'Go' for text inputs
- SHows 'Next' to number inputs

### Submit Form
> If the form has no submit button, then the implicit submission mechanism must do nothing if the form has more than one field that blocks implicit submission.
That means if you have two inputs on form without submit button, hit 'Search' button on soft keyboard won't do anything. The fix is to have a hidden submit button so 'search' button works.
