# CSS

- `max-width` means use this width if there is space to do so, otherwise take up 100% of available space.
- centre a block element inside another block element with `margin: 0 auto;`
- `:not` pseudo class allows us to negate a selector e.g. `.row:not(:last-child)`, so it is applied to all *row* except the `last-child` *row*.
- `calc()` function allows arithmetic with different units e.g. `calc(20% + 20px)`
- when using float layouts the container will collapse losing background properties and height, the clearfix technique will solve this
  ```css
  .clearfix::after {
    /* pseudo element needs content to be set */
    content: "";
    display: table;
    clear: both;  
  }
  ```

- use attribute selector `[attrib="term"] {` to select based on the value of an attribute ([MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/Attribute_selectors))
- `background-clip: text` can be used to clip a background color, gradient or image to a piece of text, the text color needs to be `transparent` so it doesn't block the background.
- `background-size` can be a percentage or value width or a keyword such as `cover` (100% width)
- `outline` and associated properties create a border around an element that takes up no space and are drawn outside of an elements content ([MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/outline))
- the direct child selector, selects only first level of children not any grand-children etc. `.container > *` will select all direct of children of `container`, `.section1 > div` selects only the direct div children
- linear gradient function `linear-gradient(to right, $color1, $color2);` can be specified with directions `to right top` or degrees `90deg`
- linear gradients can also take percentage values as stop points and multiple colors can be given allowing complex gradients `linear-gradient($c1 10%, $c2 50%, $c3 80%)` (using this technique with transparent colors you can make create interesting effects)
- 3D transforms are possible with `perspective` and `backface-visibility` properties ([Ref](https://3dtransforms.desandro.com/), [MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/perspective)). With `perspective` we can set a nominal distance to the user in order for transforms to give a 3D effect. Using `backface-visibility` the back of a 3D transformed element can be hidden.
- `background-image` allows multiple definitions separated by commas, for example an image and a gradient. Then using `background-blend-mode` they can be blended together in different ways.
- `border-radius` can be lost on parent when there is a background image on a child, can be fixed with `overflow: hidden` on the parent.
- `shape-outside` allows wrapping content around a floated element according to a defined shape, rather the default margin box (rectangle). Float needs to have dimensions height and width ([MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/shape-outside)). Not supported IE/Edge 9-2018.
- when trying to add space around a floated element avoid margin and padding and use a transform to move it.
- it is only possible to have one transform on an element, so if multiple transforms are defined the cascade will resolve only the highest precedence one only.
- transforming transitions need to match, e.g. normal state `translate(50%, 50%)` and hover `translateY(0)` won't work as intended should be `translate(50%, 0)`
- the `filter` property adds graphical effects like `blur`, `grayscale` etc.
- `object-fit` allows an image or video to be fitted to a container using various constraints e.g. aspect ratio. `object-position` complements this allowing positioning of the elements like `background-image` does.
- `input` element doesn't inherit font properties by default need to specify it `font-family: inherit`
- the border on an `input` when it is selected is the `outline` of the `:focus` pseudo-class
- when adding a `border` to a pseudo-class like `:hover` or `:focus` it can move the elements position by adding the border, get around this by adding the same size border with a transparent color to normal state of element
- the `::placeholder` pseudo-element enables styling of placeholder text on input like elements
- `:placeholder-shown` pseudo-class is the state that applies when the placeholder text is shown in an `input` or `textarea`
- `:invalid` happens when an `input` is invalid, e.g. incorrect *email* type, empty but *required* field. Firefox adds a `box-shadow` style by default.
- *sibling selectors* can select elements at the same level but lower down (never above): Adjacent `+` matches only the next sibling, and General `~` matches any lower sibling ([MDN](https://developer.mozilla.org/en-US/docs/Learn/CSS/Introduction_to_CSS/Combinators_and_multiple_selectors#Combinators_and_groups_of_selectors)).
- checkboxes and radio buttons have `::checked` pseudo-element to enable styling when checked!
- `display: none` will remove the element, if accessibility is important for the element, there are better ways to [hide an element visually](https://gomakethings.com/hidden-content-for-better-a11y)
- `visibility: hidden` doesn't draw an element, but it affects layout as if it were drawn, it isn't possible to for the element to receive focus either.
- forms require an actual button element for submits
- its common practice to have utility classes be defined as `!important` so they get they are applied with highest precedence
- an `inline-block` only takes up the space of its contents, unlike a `block` which takes up 100% of available.
- even up two columns by defining width on one at least, and floating to the appropriate side to correct the spacing
- `position: fixed` is similar to absolute in that it is removed from normal flow and positioned absolutely, it then holds that position as the pages moves/scrolls
- `background-origin` specifies how the background is positioned relative a box scheme (independent of the elements box scheme), three options `border-box`, `padding-box` and `content-box`.
- `transform-origin` is similar and defines the location where transform occur e.g. rotations.

## Sass

- can use hex colors (in variables) and place into CSS `rgba` function `rgba($color, 0.5)`
- `&` works like string substitution, allows nice BEM workflow
  ```scss
  .header {
      margin: 10px;

      &__logo { // .header__logo
          width: 100px;
      }
  }
  ```
- partials use leading underscore filename and are imported with `@import path/filename`, underscore and file extension omitted
- math operations can only work with the same units (for mixed units see CSS `calc`, need to escape SASS variables with `#{$var1}`)
- **idea**: use `z-index` variables or mixins to create layers that can be assigned to
