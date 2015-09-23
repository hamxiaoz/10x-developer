# CSS

html
```html
<link type="text/css" rel="stylesheet" href="assets/css/my.css">
<link href="mysite-mobile.css" rel="stylesheet" media="screen and (max-device-width: 480px)">

//- nav
<nav>
  <ul>
    <li><a href="#">Home</a></li>
    <li><a href="#">About</a></li>
    <li><a href="#">Contact</a></li>
  </ul>
</nav>
```
css
```css
// usually split in this way: layout.css color.css typography.css
// use one parent css to include them:
    @import url(layout.css);
    @import url(color.css);
    @import url(typography.css);
    
@media print {
        body {
            /* css text */
        }
    }
```

viewport `<meta name="viewport" content="width=device-width">`

## Tag
- `strong` vs `b` (style only)

## selector

Prefer class over id: id is only faster when id is the key selector, it's slower when `#home a`, because browser **read from right to left** so `#home a` is read as finding all `a` then pick `#home`.

[css selector specificity](http://www.htmldog.com/guides/css/intermediate/specificity/)
- `div p` win `p`
- same style, last one win
- you give every ID selector (“#whatever”) a value of 100, every class selector (“.whatever”) a value of 10 and every HTML selector (“whatever”) a value of 1. Then you add them all up and hey presto, you have the specificity value

descendant selector 
- `#id-name h2 { } /* it means select h2 under the id 'id-name' */`
- by default, it selects all nested chilren no matter how deep they are.
- to select the direct child: `#id-name > h2`

select sibling using '+'
```css
    h1+p{} // select all p comes after h1
```

the pattern of the selector: context + element + pseudo-class/elements
``` css
div#greentea > blockquote p:first-line // p is the element.
``` 

pseudo-class
- select based on state `a:link { color: green; }`
- nth-child pseudo-class:
```css
    p:nth-child(2n) { color: green; }
```
- first-child:
```css
    div.tableRow p:first-child {
        text-align: right;
    }
```

pseudo-elements
- select part of the text or line
```css
    p:first-letter { font-size: 3em; }
```

## Font
```css
font-family: Verdana, Arial, "Courier New", sans-serif;

// how to use web font (web open font format 'WOFF')?
@font-face { font-family: "name"; src: url("font.woff"), url("font.ttf"); }
```

font-size: `px` (old IE doesn't support it!), `%` (relative to the parent element), `em` (scaling to the parent element) or keywords (small/medium etc.)

to use it properly: (so it can be really easy to adjust whole font by just changing the base font)
- choose a keyword for body to define the whole page size as a basement.
- use em or %

`line-height`: it can use number only to specify the size to its *own* size.
```css
#gift { line-height: 1em; } // all elements inside gift is the same size of the element of gift, h1 size will be the same as h2! (which inherits from body)
#gift { line-height: 1; } // all elements inside gift is the same size as their own size. So h1 will be h1's size and h2 will be h2's size.
```

text-decoration: no need to use `,` for multiple value: `text-decoration: underline line-through;`

## Display

- `display:none` means the browser will render the page as the element doesn't exist. 
- `visibility:hidden` means **it renders as it's there** but not visible.

`display:block` will stretch the element to left/right as far as possible.

`width`: browser will create scrollbar if viewport is smaller, in this case, use max-width instead of width.


## Box

- padding, margin. Order matters! The last one takes precedence, overriding anyone specified before:
```css
    margin: 30px;
    margin-left: 50px; // margin left will be 50px instead of 30px
    or
    margin-left: 50px; 
    margin: 30px; // margin left will be 30px
```
- shortcuts: `top right bottom left` (how to remember: think as a clockwise direction: from 12 to 11)
```css
    margin: 30px 20px 30px 20px;
    margin: 30px // means all sides have the same padding of 30px
```
- shortcuts2: top/bottom right/left `margin: 30px 20px;`
- other shortcuts for border and background:
```css
    border: solid #009302 thin; // ... and border-width
    background: white url(images/gift.gif) repeat-x; // color image repeat
```

width: it specifies the content width, **not including padding/margin.**
```css
div {
  border: 6px solid #949599;
  height: 100px;
  margin: 20px;
  padding: 20px;
  width: 400px;
}
```
![](http://learn.shayhowe.com/assets/images/courses/html-css/opening-the-box-model/box-model.png)

text-align: it will align *all inline content* inside a block element.

## Misc

### semantic css creates more problem (redundancy) than it solves.
- what's semantic css: code what you mean, think about the structure. if it's important, put it as H1.
- read last comment from: http://news.ycombinator.com/item?id=3653540
- use less can solve the problem.
- other css framework: blueprint, 960.

### Why element.style.left doesn't work?
You need to set it to the object in Javascript or using inline style
element.style is just a conversion of the element's style attribute into a scriptable object. If you haven't set any inline style on the element, you won't get anything back.
`document.getElementById("convert").style.display = "block"` or `<a style="display: block;"></a>`


## SASS
- [style guide](http://css-tricks.com/sass-style-guide/)
- [SASS: differences between mixins, extends and placeholders](http://krasimirtsonev.com/blog/article/SASS-mixins-extends-and-placeholders-differences-use-cases))
- 使用Compass
Compass不但讓SCSS的使用更方便，還有大量的module、helper可以使用，解決cross broswer的問題並且減少重複的程式碼，增加可讀性。

## Examples
- [Form control margin](http://stackoverflow.com/questions/18562153/what-css-controls-the-right-and-left-margins-between-these-form-elements-in-twit)
- [bootstrap row click and offmenu canvas] (http://jasny.github.io/bootstrap/javascript/#fileinput)

