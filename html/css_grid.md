# CSS Grid

Links:

* cheat sheet: [https://css-tricks.com/snippets/css/complete-guide-grid/](https://css-tricks.com/snippets/css/complete-guide-grid/)
* basic: [https://developer.mozilla.org/en-US/docs/Web/CSS/CSS\_Grid\_Layout/Basic\_Concepts\_of\_Grid\_Layout](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout/Basic_Concepts_of_Grid_Layout)
* CSS Grid examples: [https://gridbyexample.com/](https://gridbyexample.com/)
* CSS examples: [http://labs.jensimmons.com/](http://labs.jensimmons.com/)

Playground: [https://jsfiddle.net/hamxiaoz/7vo3mzkw/](https://jsfiddle.net/hamxiaoz/7vo3mzkw/)

Grid methods:

* row/bootstrap: The reason that our legacy methods need row wrappers is because we are faking a grid by assigning widths to items. We then pull and push the items around to make gaps between them.
* float based: In a float based grid, you need to wrap the elements that make up each row, and clear the row in order that things in the next row don’t float up.
* Flex box based: In a flex based grid you need your row to define a new flex container, or you need to get very clever with wrapping, flex-basis and margins to get the same effect without.
* Grid: doesn’t need these row wrappers because you have defined row tracks, and lines to position items against. There is no danger of grid items hopping up into the row above. If you define row wrappers then each row becomes a new one-dimensional grid layout, and there is little benefit to using Grid over Flexbox if you limit yourself to a single dimension.
* CSS Grid vs CSS Flexbox: Flexbox is hard to align multiple item gutters on different rows, especially if you have one flex item hidden. Actually Flexbox is a **one direction** layout method, where CSS grid is **two-dimentional**.

## Concept

* grid lines: starts from 1 \(not 0\)
  * name grid line: `grid-template-columns: [linename1] 100px [linename2 linename3];`
* position items by lines \(not track\)
* grid track: space between any lines
* grid area: rectangle between lines
  * use this for naming col and rows: `grid-template-area: 'a b'` \(use with `grid-area: a`\)

position items:

* container: `align-items` and `justify-items`
* child: `align-self` and `justify-self`

area name:

* container: `grid-template-areas: name-without-quote` \(can be used toghther with `grid-template-columns`\)
* child: `grid-area`

