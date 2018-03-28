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
- `outline` and associated properties create a border around an element that takes up no space and are drawn outside of an elements content ([MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/outline))
- the direct child selector, selects only first level of children not any grand-children etc. `.container > *` will select all direct of children of `container`, `.section1 > div` selects only the direct div children
- linear gradient function `linear-gradient(to right, $color1, $color2);` can be specified with directions `to right top` or degrees `90deg`
- 3D transforms are possible with `perspective` and `backface-visibility` properties ([Ref](https://3dtransforms.desandro.com/), [MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/perspective)). With `perspective` we can set a nominal distance to the user in order for transforms to give a 3D effect. Using `backface-visibility` the back of a 3D transformed element can be hidden.
- `background-image` allows multiple definitions for example an image and a gradient. Then using `background-blend-mode` they can be blended together in different ways.
- `border-radius` can be lost on parent when there is a background image on a child, can be fixed with `overflow: hidden` on the parent.


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

