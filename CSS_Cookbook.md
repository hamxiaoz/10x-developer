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

And you want to adjust the margin under the root class `.native`:

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

You can use `&`:

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
- Refer to the parent

  ```less
  // -> .some-class.another-class
  .some-class {
    &.another-class {}
  }

  // -> .button:hover {}
  .button {
    &:hover {}
   }
  ```
  
- Reposition the parent selector to specified class

  ```less
  // -> body.page-about .button {}
  .button {
    body.page-about & { }
  }
  ```

# How to add search icon to input?
http://codepen.io/hamxiaoz/pen/MJdXyo
- Could not use ::before because input doesn't have content
- Position icon in input, and make it vertically center with top and translateY
- Padding left on input for space of the icon
