# Advanced CSS - Course Notes

Based around Udemy's [Advanced CSS Course](https://www.udemy.com/advanced-css-and-sass/)

- Course [repository @ Github](https://github.com/jonasschmedtmann/advanced-css-course)
- Jonas [resource site](http://codingheroes.io/resources/)

## 2 - Natours Part One

Start building the Natours landing page.

### 2.5 - Header P1

- Browser consistency regarding initial css state is getting better, less need for *normalize*. Using the universal selector `* { ... }` to do a basic reset will work well.
- The `box-sizing` property allows us to change the css box model. By default it is `content-box` meaning the width and height of a box apply to the contents and any padding or border are added on to this size. Using `border-box` then the width and height include any padding and border, giving the total width and height as defined.
- Set the global font settings in the *body* element to utilize css inheritance, so they apply to all children of body. If they were added to the universal selector than they would be applied to each element rather than being inherited.
- Setting the `line-height: 1.5;` means that the line height is to be one and half times the size of the default line-height.
- `height: 90vh;` sets the height to 90% of the viewport height, ensuring that the element is the same percentage of the viewable area.
- `background-position` anchors the background to a part of the viewport, *top* will keep the top of the background intact in the same position no matter who the viewport is resized. Other parts of the background will be cropped to facilitate this.
- `linear-gradient` takes two color arguments to define the transition and also direction arguments, `linear-gradient(to right bottom, #333, #111)`
- use `clip-path` to clip the contents of an element to a given shape, for example `polygon`. Give the coordinates of the clip path, where the origin is the top left.

### 2.6 - Header P2

- As `<img>` is an inline element, it is good practice to wrap it in a container `<div>` and then position that.
- The position of an absolutely positioned element is based on the first parent that has relative positioning.
- It makes sense to control the height of elements rather than width, for example setting the height of an image and letting width be set automatically.
- The first `<h1>` is the main title of the page, important for search engines. It may be necessary to split up text in spans so the design is right and also so that text looks good for search results.
- Change the case of text with `text-transform: none | capitalize | uppercase | lowercase`.
- Block elements use all horizontal space available to them and creates a vertical break.
- `letter-spacing` as it suggests specifies how much space there should be between letters in text.
- To centre a block element in both dimensions, use absolute position and translate. First, position 50% top and left, this will offset the top left corner of the box with respect to the parent. Then add a translation of -50% in x & y, this will shift the box back 50% of its own height and width.

    ```css
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    ```

### 2.7 - Animations

- Animations use `@keyframes` to define properties over the period of the animation.
- Performance is optimized when animating `opacity` and `transform`, recommenend to limit to these two.
- Specify *keyframes* by defining percentage of animation time and setting properties.

    ```css
    @keyframes moveInLeft {
        0% {
            opacity: 0;
            transform: translateX(-100px)
        }

        80% {
            transform: translateX(10px)
        }

        100% {
            opacity: 1;
            transform: translate(0);
        }
    }
    ```

- The same animation can be used in different places by referencing its name.
- The animation is applied to the desired element by setting the `animation-name` property on the element.
- The animation can be customized further using the other *animation* properties:

    ```css
    animation-duration: 1s;
    animation-timing-function: ease-out;
    animation-delay: 3s;
    animation-iteration-count: 3;
    ```
- The shorthand `animation` property can also be used to combine many of the other properties
- Jerkiness or stutter may sometimes be observed with animations, a solution in some cases is to use `backface-visibility: hidden`
- [MDN Animation Reference](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Animations)
- Often full CSS animations are unnecessary and simple CSS transitions will do, they can be used to set the speed of the change between two properties
- The shorthand property is the easiest to use 
    ```css
    transition: width 2s, height 2s;
    ```
- [MDN Transition Reference](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Transitions)

### 2.8 - Animated Button P1

- An *inline-block* is a block element that is flowed like a single inline element - [MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/display) (depreacted now?)
- **Psuedo classes** allow different styling for special states of an element
- For an `<a>` element we have pseudo-classes like `:link`, `:visited`, `:active` and `:hover`
- When transforming in pseudo classes the movement is relative to inital `:link` not previous state
- CSS *transition* effects need to be defined on the `:link` class, and the actual desired values in the other states
- Specify a shadow on an element with `box-shadow` with the attributes `offset-x offset-y blur-radius spread-radius color`
- Multiple shadow effects can be added on the same property and will overlay each other

### 2.9 - Animated Button P2

- **Pseudo elements** allow a particular part of an element to be styled differently, for example `::first-line`, `::selection`, `::after` or `::before`
- Using double colons to distinguish *pseudo-elements* from *pseudo-classes*
- `::after` essentially adds a virtual element after the element in question
- *pseudo-elements* are treated as children of the element, so `height: 100%` will be same as original element
- Its also required to provide a `content: ""` property even if its empty and also a display property
- *pseudo-elements* can be applied to *pseudo-classes* example `.button:hover::after`
- `animation-fill-mode` property sets the default animation state, `backwards` value means the element takes on the *0%* keyframe while the delay is in effect and proceeds with the animation from there

## 3 - CSS Behind the Scenes

Get a better understanding of how CSS actually works.

### 3.12 - Three Pillars of Good HTML & CSS

1. Responsive Design
   - fluid layouts
   - media queries
   - responsive images
   - correct units
   - desktop-first vs mobile-first
2. Maintainable & Scalable Code
   - Clean
   - Easy-to-understand
   - Growth
   - Reusable
   - CSS file organization
   - CSS class naming
   - HTML structure
3. Web Performance
   - Limit request, fewer files
   - Less code and compressed
   - CSS preprocessor
   - Limit images and compress

### 3.14 - CSS Parsing P1

- Terminology of a CSS rule:
   - composed of a *selector* and a *declaration block*
   - each *declaration* is a **property** and its **declared value**
- When a webpage is parsed, in addition to parsing HTML and creating the DOM the CSS is also parsed into the CSSDOM
  - two steps to CSS parsing, *resolving the cascade* and *calculating find values*
- multiple sources of CSS: *Author (developer)*, *User*, *Browser (user-agent)*

**The Cascade** is the process combining stylesheets and resolving conflicts between the rules and declarations that apply to multiple elements.
Conflicts are resolved based on *Importance* > *Specificity* > *Source Order*.
- **Importance**
   1. User `!important`
   2. Author `!important`
   3. Author declarations
   4. User declarations
   5. Default browser declarations
- **Specificity**
   1. Inline styles
   2. IDs
   3. Classes, pseudo-classes, attribute
   4. Elements, pseudo-elements
- **Source Order** declarations will have precedence based on position in file, higher in source has highest precedence.

**Points to remember about the Cascade**
  - declarations marked with `!important` has highest priority
  - use `!important` as a last resort, specificities are better solution
  - inline styles will override any external stylesheets, but are poor practice
  - a selector with **one** ID is more specific than one with *1000* classes
  - a selector with **one** Class is more specific than one with *1000* elements
  - the universal selector `*` has no specificity and will always have lowest precedence
  - better to rely on *specificity* than on *order* of selectors, code refactoring can easily destroy any ordering making the code less maintainable, with one exception:
    - when relying on third party stylesheets, you need to rely on order by putting your own stylesheets below the third party ones


- a more specific selector will always have higher precedence, even when it may not look like it
  - it is possible that an anchor declaration could be more specific than its associated *hover* declaration resulting in the *hover* declaration never being applied.
  ```css
  /* 1 id, 2 classes, 2 elements */
  #nav div.pull-right a.button {
      background-color: green;
  }
  /* 1 id, 2 classes, 1 elements */
  #nav a.button:hover {
      background-color: yellow;
  }
  ```

### 3.16 - CSS Parsing P2

CSS unit values are converted to final actual pixel values, using six steps.

1. **Declared** Any rules declaring this value.
2. **Cascaded** The value that has been cascaded from all declared.
3. **Specified** The default or initial value if there is nothing from cascade.
4. **Computed** Relative values are converted to absolute (percentages are not classed as relative).
5. **Used** Is the final value calculation, like *66%* of parent's width, for example `102.4px`.
6. **Actual** Browser and device interpretation of the Used value, rounded for example `102px`.

Browsers specify a **root** `font-size` for each page, usually 16px.

**Percentages** are treated differently for fonts and dimensions.
- fonts will use their parents font size to calculate a percentage
- dimensions like *padding* will use their parent's **computed width**

**Font-Based Values** also depend on the type of property they being used with.
- `em` units with fonts are relative to their parent's computed font-size
- using `em` with lengths means they are relative to the **current element's** computed font-size
- `rem` unit is the same for fonts or lengths, and is relative to the root computed font-size

**Viewport** units are `vh` and `vw` are simply a percentage of the browser viewport width and height.

### 3.17 - CSS Parsing P3

 Certain properties can inherit values from their parents. As a rule of thumb all font related properties can be inherited. See the documentation of a property to see if it can be inherited.

 If there is a cascaded value for a property than that is used in the calculation of the final value, and inheritance is not considered.

 If there isn't any cascaded value and the property supports inheritance then the **computed** value of the parent is used for the child, not the relative value that may be specified on the parent.

 With no cascaded value and no inheritance than the default initial value defined for the property will be used.

 Inheritance can be forced with the `inherit` keyword. The properties default value can also be forced with the `initial` keyword.

 ### 3.18 - Pixel to `rem` Workflow

Better to use relative units for responsive design. Using `em` can be difficult as it can require calculations on the parent and current element.

A simpler solution is to use `rem` units and set a root `font-size` with the `html` selector. Calculations can be made easier by using `10px` as the root `font-size`, so that `1rem` is equal to `10px`, `3rem` is `30px` etc.

This workflow greatly aids responsive designs, as the layout can be controlled by just the root `font-size` making media queries much simpler to define.

Setting the root `font-size` in pixels is bad practice though as it will override any user styles. A better approach is to use a percentage of the browsers default size (generally `16px`), so setting root `font-size: 62.5%` will be equivalent to `10px` when the default browser value is used. This way any custom user styles will still have an effect.
 
 It should be noted that `rem` units are not supported in IE 9 or below. There are some known issues with certain properties and browsers ([caniuse.com](https://caniuse.com/#feat=rem)).

 