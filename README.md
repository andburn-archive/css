# Advanced CSS - Course Notes

Based around Udemy's [Advanced CSS Course](https://www.udemy.com/advanced-css-and-sass/)

- Course [repository @ Github](https://github.com/jonasschmedtmann/advanced-css-course)
- Jonas [resource site](http://codingheroes.io/resources/)

## 2 - Natours Part One

Start building the Natours landing page.

### 2.5 - Header P1

- Browser consistency regarding initial css state is getting better, less need for *normalize*. Using the universal selector `* { ... }`to do a basic reset will work well.
- The `box-sizing` property allows us to change the css box model. By default it is `content-box` meaning the width and height of a box apply to the contents and any padding or border are added on to this size. Using `border-box` then the width and height include any padding and border, giving the total width and height as defined.
- Set the global font settings in the *body* element to utilize css inheritance, so they apply to all children of body. If they were added to the universal selector than they would be applied to each element rather than being inherited.
- Setting the `line-height: 1.5;` means that the line height is to be one and half times the size of the default line-height.
- `height: 90vh;` sets the height to 90% of the viewport height, ensuring that the element is the same percentage of the viewable area.
- `background-position` anchors the background to a part of the viewport, *top* will keep the top of the background intact in the same position no matter who the viewport is resized. Other parts of the background will be cropped to facilitate this.
- `linear-gradient` takes two color arguments to define the transition and also direction arguments, `linear-gradient(to right bottom, #333, #111)`
- use `clip-path` to clip the contents of an element to a given shape, for example `polygon`. Give the cordinates of the clip path, where the origin is the top left.

### 2.6 - Header P2

- As `<img>` is an inline element, it is good practice to wrap it in a container `<div>` and then position that.
- The position of an absolutely positioned element is based on the first parent that has relative positioning.
- It makes sense to control the height of elements rather than width, for example setting the height of an image and letting width be set automatically.
- The first `<h1>` is the main title of the page, important for search engines. It may be necessary to split up text in spans so the design is right and also so that text looks good for search results.
- Change the case of text with `text-transform: none | capitalize | uppercase | lowercase`.
- Block elements use all horizontal space available to them and creates a vertical break.
- `letter-spacing` as it suggets specifies how much space ther should be between letters in text.
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
- Often full CSS animations are unecessary and simple CSS transitions will do, they can be used to set the speed of the change between two properties
- The shorthand property is the easiest to use `transition: width 2s, height 2s;`
- [MDN Transition Reference](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Transitions)

### 2.8 - Animated Button P1

- An *inline-block* is a block element that is flowed like a single inline element - [MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/display) (depreacted now?)
- **Psuedo classes** allow different styling for special states of an element
- For an `<a>` element we have psuedo-classes like `:link`, `:visited`, `:active` and `:hover`
- When transforming in psuedo classes the movement is relative to inital `:link` not previous state
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

