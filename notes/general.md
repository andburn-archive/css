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

