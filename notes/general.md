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
