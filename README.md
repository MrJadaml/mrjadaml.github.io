# CSS

### Objectives
* Explain the purpose of CSS
* Know where CSS goes, and why it goes there
* Explain what a *selector* is
* Describe the *box model*
* Know where to turn to debug CSS

<hr>

### CSS Definition
CSS defines the look and presentation of an HTML doc. It controls the colors, fonts,
layout, and other styles.

#### Resources:
* [CSS-Tricks](https://css-tricks.com/)
* [MDN](https://developer.mozilla.org/en-US/docs/Web/CSS)
* [WPD](https://docs.webplatform.org/wiki/Main_Page)

<hr>

### Where does CSS come from?

There are main places that CSS will *cascade* from:
* Browser defaults
  * Also known as *user agent* Styles
* User defined Styles
  * Editing the browser's default styles (chrome extensions)
* Page authored styles
  * The ones you write for your web site!

<br>


Reset browser default "user agent" styles with [Eric Meyer's CSS Reset](https://css-tricks.com/snippets/css/meyer-reset/)
 * Here's a minified one-liner to place at the top of youry main CSS file


 ```css
html,body,div,span,applet,object,iframe,a,abbr,acronym,address,big,cite,code,del,dfn,em,font,img,ins,kbd,q,s,samp,small,strike,strong,sub,sup,tt,var,dl,dt,dd,ol,ul,li,h1,h2,h3,h4,h5,h6,pre,form,fieldset,input,textarea,label,legend,p,blockquote,table,caption,tbody,tfoot,thead,tr,th,td{margin:0;padding:0;border:0;outline:0;font-weight:inherit;font-style:inherit;font-size:100%;font-family:inherit;vertical-align:baseline;}body{line-height:1;color:black;background:white;}:focus{outline:0;}table{border-collapse:collapse;border-spacing:0;}caption,th,td{text-align:left;font-weight:normal;}fieldset,img{border:0;}address,caption,cite,code,dfn,em,strong,th,var{font-style:normal;font-weight:normal;}ol,ul{list-style:none;}h1,h2,h3,h4,h5,h6{font-size:100%;font-weight:normal;}blockquote:before,blockquote:after,q:before,q:after{content:"";}blockquote,q{quotes:"" "";}abbr,acronym{border:0;}
 ```
Short of the CSS reset, browser and user defaults are out of your hands. The last one in the list, "Page authored styles", is where you come into play.

### Implementation

We have three options of where to write our CSS:
* Inline
* Style tags
* External style sheets


* **Inline?**
```html
<div style="color: purple; height: 20px;"></div>
```
Avoid this method of styling. It's considered bad practice and can introduce unexpected results.

<br>

* **Style tag?**
```html
<!DOCTYPE html>
<html>
  <head>
	  <style>
      .some-class {
        color: blue;
      }
      #some-id {
        margin-right: 40px;
        color: rgba(77, 57, 75, 1);
      }
    </style>
  </head>
  ...
```
Not the best choice, but for quick testing and mock-ups can be useful.

<br>

* **External stylesheet?**
<blockquote>./index.html</blockquote>
```html
<html>
    <head>
      <title>Super Cool Web Page</title>
      <link rel="stylesheet" href="css/some-stylesheet.css">
    </head>
    <body>
      ...
    </body>
</html>
```
The `<link rel="stylesheet" href="css/some-stylesheet.css">` is the important line here.
<blockquote>./some-stylesheet.css</blockquote>
```css
.some-class {
    color: blue;
}
.another-class {
    background-color: inherit;
    height: 42px;
}
#some-id {
    margin-right: 40px;
    color: rgba(77, 57, 75, 1);
}
body {
    width: 80%;
}
```
We have a winner!

<br>

Separating the code responsible for our presentation (CSS), from the code that defines our content (HTML) is beneficial for a couple of reasons.

* One place to find anything related to styling
* Easier to navigate and maintain
* Less duplication of code

### CSS Anatomy

```css
selector {
  property-name: value;
  property-name: value;
}
```

Let's try using some basic CSS properties:

* ``background-color: <color>;``
* ``color: <color>;``
* ``border: <br-width> <br-style> <br-color>;``

### Selectors
#### Element Selector

```css
div {
  border: solid green;
}
```
Our selector here is the `div` *element*. In this example we'll be targeting all of the `div` elements in our page and applying a green border to them.

<br>

#### Class Selector

```css
.pink-text {
  color: pink;
}
```

The class selector is denoted by a `.` before its name `pink-text`. Classes are defined with the HTML class attribute: `<div class="pink-text>"`

<br>

#### ID Selector

```css
#grey-background {
  background-color: grey;
}
```
The ID selector is denoted by a `#` before its name `grey-background`. IDs are defined with the HTML ID attribute: `<div id="grey-background>"`

IDs are used to uniquely identify elements. It's considered bad practice to apply the same ID to multiple elements.

You should rarely need to use IDs. They can create unexpected behavior due to ID collisions, are hard to track down and annoying.

#### Chained Selectors

```css
.red-text.light {
  color: lightsalmon;
}
```

We can use multiple selectors chained together. `.red-text.light` selects only elements that have both the `red-text` AND `light` classes. Elements with just one or the other will not have the `lightsalmon` color applied.

#### Multi selectors

```class
html, body {
  width: 100%;
}
```

Comma separated selectors will apply the defined styles to all selectors used. Here both the `<html>` and `<body>` elements will have a width of 100% applied to them.

<br>

#### References:

[Great Resource: 30 CSS Selectors to Learn](http://code.tutsplus.com/tutorials/the-30-css-selectors-you-must-memorize--net-16048)

[MDS's full list of CSS selectors](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference)

[CSS Specificity Guide](http://cssspecificity.com/)

<hr>

### Box Model
Elements in a web page are modeled as boxes. The content of an element dictates the initial amount of space it takes up.
```html
<p>I AM IN THE FIRST PARAGRAPH ELEMENT</p>

<p>I AM IN THE SECOND PARAGRAPH ELEMENT WITH ALL THIS EXTRA CONTENT!!!! Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.</p>
```
[JS Bin](http://output.jsbin.com/dicakuwaxi) Show with Pesticide*

* They have a content box(element) with a height and width
* Padding then surrounds the element
* A border around the padding
* Finally a margin around the border

![box-model](http://f.cl.ly/items/3n3S1L2G342K0V3k3S3v/Screen%20Shot%202015-08-08%20at%2010.51.12%20PM.png)

Check out the CSS box model with *Chrome Dev Tools*.
* OPT + CMD + i
* Right-click -> Inspect Element
* Menu Bar -> View -> Developer -> Developer Tools

* *Computed* tab*

#### Block-level & Inline Elements

**Inline**
* span
* a
* img
* i, em, b, strong
* [Many more...](https://developer.mozilla.org/en-US/docs/Web/HTML/Inline_elemente)

**Block-level**
* div
* body
* form
* p
* [Many more...](https://developer.mozilla.org/en-US/docs/Web/HTML/Block-level_elements)

the CSS attribute `display` can be used to set a block-level element to inline, and vice versa.
You can even get the best of both worlds with the `display` value of `inline-block`

<hr>

### Debugging + Good Practices
#### Debugging:
When it all goes to hell, and it will...
Chrome dev tools will be your best friend for debugging CSS.
* Elements tab
  * View node tree of elements
  * Click on an element to get more details
  * Live editing of HTML: Right-click -> Edit HTML
  * Quick interactive node path at bottom of window
* Magnifying glass icon
  * Hover over elements on page to see individual box-model overlays
  * Click on element to target it in node tree view
* Styles tab
  * Displays list of selected element's Styles
  * Live editing/preview of styles
    * Toggle styles on and off
  * Pin icon expands "state" styles (`:hover` etc.)
  * Element's box-model visual at the bottom

[Pesticide](https://chrome.google.com/webstore/detail/pesticide-for-chrome/bblbgcheenepgnnajgfpiicnbbdmmooh?hl=en-US) is another great tool for debugging CSS issues.
* Adds borders to all elements on the page for quick visual reference.

#### Good Practices
There are two things you should consider doing every time you new up a CSS doc that will help you avoid banging your head against the wall over dumb CSS issues.

* Revert to classic a classic box model setup by dropping in this bit of code:
```css
html {
    box-sizing: border-box;
}
*, *:before, *:after {
    box-sizing: inherit;
}
```
Includes borders as part of the element's size.
