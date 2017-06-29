# CSS/LESS/SASS Cookbook

## How to center ul?
Make `ul` `display: inline-block` in a `text-align: center` div 
http://codepen.io/hamxiaoz/pen/egLOwV

## How to reposition the class under specified parent in SASS/LESS?
For example you have:

```less
.parent1 {
  .parent2 {
    .container {
      margin: 5px 0;
    }
  }
}
```

And you want to adjust the margin under the **root class** `.native`:

```less
.native {

    .parent1 {
      .parent2 {
        .container {
          margin: 10px 0;
        }
      }
    }
}
```

You can use `&` [LESS: Parent Selectors](http://lesscss.org/features/#parent-selectors-feature):

```less
.parent1 {
  .parent2 {
    .container {
      margin: 5px 0;
      
      .native & {   // -> it turns to: .native .parent1 .parent2 .container {}
        margin: 10px 0;
      }
    }
  }
}
```

Usages of `&`:
- When `&` is placed **before** an element, it refers to the immediate parent

```less
// -> .some-class.another-class
.some-class {
  &.another-class {}
}

// -> .button:hover {}
.button {
  &:hover {}
  }
  
.a {
  .b {
    // -> .a .b.b1 (not .a.b1 .b)
    &.b1 {
      color: red;
    }
  }
}
```
  
- When `&` is placed **after** a selector, that selector becomes the root selector and `&` represents the whole path and the whole path is repositioned under the root selector.

```less
// -> body.page-about .button {}
.button {
  body.page-about & { }
}

.a {
  .b {
    // -> .root .a .b 
    .root & {
      color: black;
    }
    // -> .a1.a .b
    .a1& {
      color: red;
    }
    // -> .a .b.b1
    &.b1 {
      color: yellow;
    }
  }
}
```

## How to add search icon to input?
http://codepen.io/hamxiaoz/pen/MJdXyo
- Could not use ::before because input doesn't have content
- Position icon in input, and make it vertically center with top and translateY
- Padding left on input for space of the icon

## Form control margin
http://stackoverflow.com/questions/18562153/what-css-controls-the-right-and-left-margins-between-these-form-elements-in-twit

## Bootstrap: row click and offmenu canvas
http://jasny.github.io/bootstrap/javascript/#fileinput
