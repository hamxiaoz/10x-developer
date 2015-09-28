# CSS

Basic structure
```jade
<!DOCTYPE html>
html
  head
  body
    header
      nav
    section
     article
    aside
    footer
```

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
- When setting margin, often you want to reset the last one
```css
.nav li {
    display: inline-block;
    margin: 0 10px;
}
.nav li:last-child {
    margin-right: 0;
}
```

## Good to know
- `dl` `dd`
- List:  the only element we can place as a direct child of the `<ul>` and `<ol>` elements is the `<li>` element
- `audio`
```
<audio controls>
      <source src="jazz.ogg" type="audio/ogg">
      <source src="jazz.mp3" type="audio/mpeg">
      <source src="jazz.wav" type="audio/wav">
      Please <a href="jazz.mp3" download>download</a> the audio file.
</audio>
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

## Background

- Background shortcut: `background-color`, `background-image`, `background-position` and `background-repeat`
```
div {
  background: #b2b2b2 url("alert.png") 20px 10px no-repeat;
}
```

- Linear gradient is background-image 
    - [MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/linear-gradient)
    - [degrees!](http://www.quirksmode.org/css/images/angles.html)
```
div {
    background: linear-gradient( 45deg, blue, red ); 
}
```
- [`{background-size: cover/curtain/etc}`](https://developer.mozilla.org/en-US/docs/Web/CSS/background-size)

## Image
- By default it's inline element

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

## Layout

无论多么复杂的布局，其基本出发点均是：“如何在一行显示多个div元素”

### float
- Origin: was originally designed to float image to allow content to wrap around images. NOT intended for positioning or layout.
- A floated box is positioned within the normal flow, then taken out of the flow and shifted to the left or right as far as possible.
- 尽管它被taken out了, 但是其他元素还是会尊重它的box model. 不会有重叠, 这也是float最初用来图文排版的初衷.
- Being taken out, this causes the width of that element to default to the width of the content within it. 
- `float` might change the element's `display` property
- `float` usually come with `clear`: The clear CSS property specifies whether an element can be next to floating elements that precede it or must be moved down (cleared) below them. The clear property applies to both floating and non-floating elements.
    - `clear` affects the applying element, not other elements
- 假如某个div元素A是浮动的，如果A元素上一个元素也是浮动的，那么A元素会跟随在上一个元素的后边(如果一行放不下这两个元素，那么A元素会被挤到下一行)；如果A元素上一个元素是标准流中的元素，那么A的相对垂直位置不会改变，也就是说A的顶部总是和上一个元素的底部对齐
- how to fix layout using float issues: `overflow: auto` or clear fix, [See here](http://learn.shayhowe.com/advanced-html-css/detailed-css-positioning/)

REF
- http://www.smashingmagazine.com/2007/05/css-float-theory-things-you-should-know/
- [经验分享：CSS浮动(float,clear)通俗讲解](http://www.cnblogs.com/iyangyuan/archive/2013/03/27/2983813.html)

Layout Examples using float or inline-block
- [2 columns using float left and right](http://codepen.io/hamxiaoz/pen/WQGOZm)
- How about 3 columns? float left for all and assign width.
- layout using inline-block

Other usage:
- you can float li in ul so 4 lis will be in the same row ( http://dashinsky.com/designer-news-statistics/)
    - or `li { display: inline-block;}`
- or float the badge: see gist revision number.

### position
- `position:static`
    - default
    - means it's **not positioned**.
- `position:relative` 
    - it's still static, where **it can be offset** by adding other property such as top:-20px etc
- `position:fixed` 
    - 脱离文件流 
    - means it's always staying in the same place, even the page is scrolled.
    - 应用:比如onboard时做tutorial, 又比如nav-top-fixed, 又比如[知乎专栏的logo, 那个'知'字](http://zhuanlan.zhihu.com/intelligence/19874517)
- `position:absolute` 
    - 脱离文件流  
    - is the trickiest position value. absolute behaves like fixed **except relative to the document, or to the nearest absolute or relative parent.**
    - absolute是基于父级元素的定位，当父级元素是relative的时候，absolute的元素就会是基于它的定位了。比如你可以让一个按钮始终显示在一个元素的右下角。





### float和position的区别, 等
>原来是用float来在一排并列各个div的, 但是现在可以用display:inline-block来做, 更简单.
注意: inline-block elements are affected by the vertical-align property, which you probably want set to top.

> 我们常说的文档流其实是指默认文档流。基本显示模型block和inline分别是块狀换行和连续多行模型，前者可以设定尺寸，后者不可以设定尺寸（根据内容决定尺寸和折行）。
不过我们总是遇到固定尺寸，或者固定部分尺寸且不折行的场景，这个时候我们马上会想到使用float来做布局，因为float会触发shrink to fit特性，实现根据内容决定尺寸，float还不会产生折行，我们通过clear来手工模拟折行。
很多时候我们希望控制的布局流问题不需要float和position实现，而应该通过显示模型定义来解决。比如现在的column layout、flex box等等，都是在这个角度解决我们遇到的问题，它们应该才是正解。

> Mobile上面那么你就知道为啥**float很少在布局上使用**。Android和iOS里面的flex box已经非常稳定了，很低版本（Android 1.6，iOS 3）就已经很好支持了，用这些布局模型在窄小且多样的手机屏幕上面相当可靠，而float在这些情况下则问题层出不穷。所以我现在相信mobile first，也相信移动设备的Web能够更好的推广CSS3的众多新特性的采用。比如新的CSS3 background and box module在移动设备里面几乎是必备的，因为background-size是retina display必用的，**而border-image则是解决复杂的按钮和面板的最佳解决方案**。如果你做Mobile Web，那么你就会爱上CSS3新特性，也会享受它带来的标准化的世界的好处。

position和float的区别:
> float对应的其实是传统印刷排版中图文混排中的环绕。这其实可以理解，因为CSS的模型和术语脱胎于传统排版，故而与计算机GUI技术通常基于组件的模型相差甚远。还有，CSS box model中，width/height不算入padding和border，许多开发者对这点很不适应，这实际上是GUI的控件思维与CSS排版思维的冲突。

> 再说position布局。position其实比float要更接近“布局”属性。但是position的问题是，**所谓布局是设定各区域（元素）的关联和约束，而定位只是设定单一元素的位置大小** (问题的本质!!!)。要实现一个布局，要对多个定位元素中手动设定相关的参数（如左栏width:200px，右栏left:200px），相当于人为的把大小和位置参数计算出来。这违背了DRY原则，也无法真正实现关联约束。（如左栏设了max/min-width之后，最终实际width未必是200px，此时右栏怎么设left值？又如一个水平固定width、垂直自适应height的绝对定位元素，我们如何从它的底部继续排下一个元素？）除非我们引入JavaScript脚本来进行计算。因此运用position布局的限制条件相当多，通常只适合那些相对孤立的部件（如页头页脚）或较为简单且各区域大小位置固定的布局。至于说以JavaScript实现的布局管理器，是将position作为实现布局的底层技术，已经算不得CSS了（因为你也不写CSS）。

> position不是用来做布局。float是传统css布局手段
float能让元素从文档流中抽出，它并不占文档流的空间，典型的就是图文混排中文字环绕图片的效果了。并且float这也是目前使用最多的网页布局方式。不过需要注意的是清除浮动是你可能需要注意的地方。并且如果你要考虑到古老的IE6之类的还会有一些bug诸如双边距等等问题。
而position顾名思义就是定位。他有以下这几种属性：static(默认)，relative(相对定位)，absolute(绝对定位)和fixed(固定定位)。其中static和relative会占据文档流空间，他们并不是脱离文档的。absolute和fixed是脱离文档流的，不会占据文档流空间。

> 比较可以发现，float和position最大的区别其实是是否占据文档流空间的问题。虽然position有absolute和fixed这两个同样不会占据文档流的属性，但是这两个并不适合被用来给整个网页做布局。为什么？因为这样你就得为页面上的每一个元素设置一个xy坐标来定位。



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

