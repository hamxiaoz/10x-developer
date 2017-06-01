# Flexbox
Use this as reference: https://css-tricks.com/snippets/css/a-guide-to-flexbox/

## Q&A

#### What is it?
It's a container used to layout items. We used to use `float` to layout.

#### Do I still need to use `max-width`?
Yes.

#### How to use it ot replace bootstrap?
- For `col-md-3`, use percentage: `flex-basis: 25%`.
- For `pull` or `push`, use `order: n` (by default is 0, 1 will move the item on main axis)
- For `visible-xs`, use CSS `display:none` on different breakpoints. Note this has nothing to do with Flexbox

## Notes


## Other resources
- practice: https://flexboxfroggy.com/
