# Core

CF-Core acts as the backbone for Capital Framework. It's made up of four child components `cf-vars`, `cf-media-queries`, `cf-utilities`, and `cf-base`.

## Vars

Theme variables for setting the color and sizes throughout the project. Overwrite them in your own project by duplicating the variable `@key: value`.

Ex. to set your base font size, add `@base-font-size-px: 17px;` to your project.

### Sizing variables

```
@base-font-size-px:   16px;
@base-line-height-px: 22px;
@base-line-height:    unit(@base-line-height-px / @base-font-size-px);
@bp-xs-max:           600px;
@bp-sm-min:           @bp-xs-max + 1px;
@bp-sm-max:           900px;
@bp-med-min:          @bp-sm-max + 1px;
@bp-med-max:          1020px;
@bp-lg-min:           @bp-med-max + 1px;
@bp-lg-max:           1230px;
@bp-xl-min:           @bp-lg-max + 1px;
```

### Color variables

`$color-` variables are from 18F's [US Web Design Standards](https://github.com/18F/web-design-standards/blob/18f-pages/assets/_scss/core/_variables.scss)

```
// body
@text:                   #212121; // $color-base

// a
@link-text:              #0071bc; // $color-primary
@link-underline:         #0071bc; // $color-primary
@link-text-visited:      #4c2c92; // $color-visited
@link-underline-visited: #4c2c92; // $color-visited
@link-text-hover:        #205493; // $color-primary-darker
@link-underline-hover:   #205493; // $color-primary-darker
@link-text-active:       #046b99; // $color-primary-darkest
@link-underline-active:  #046b99; // $color-primary-darkest

// table
@table-border:           #5b616b; // $color-gray

// thead
@thead-text:             @text;
@thead-bg:               #f1f1f1; // $color-gray-lightest

// input
@input-bg:               #fff;
@input-border:           #5b616b; // $color-gray
@input-border-focus:     #3e94cf; // $color-focus
@input-placeholder:      grayscale(#c7336e);

// .figure__bordered
@figure__bordered:       #d6d7d9; // $color-gray-lighter
```

## Media Queries

Mixins for consistent media queries that take `px` values and convert them to `em`s.

### Min and max width media queries

These mixins take a `px` value breakpoint and set of style rules and converts them to the corresponding min or max width media query.

```
.respond-to-min(@bp, @rules);

.respond-to-max(@bp, @rules);
```

Ex.
```
.respond-to-min( @bp-sm-min, {
    .title {
        font-size: 2em;
    }
} );

// Compiles to

@media only all and (min-width: 37.5625em) {
    .title {
        font-size: 2em;
    }
}
```

### Range media queries

This mixin takes both min and max `px` values and a set of style rules and converts them to the corresponding min and max media query.

```
.respond-to-range(@bp1, @bp2, @rules);
```

Ex.
```
.respond-to-range( @bp-sm-min, @bp-sm-max, {
    .title {
        font-size: 2em;
    }
} );

// Compiles to

@media only all and (min-width: 37.5625em) and (max-width: 56.25em) {
    .title {
        font-size: 2em;
    }
}
```


## Utilities

### Helper classes

#### JS only

Hide an element when JavaScript isn't available. Requires a small script in the HEAD of your HTML document that removes a `.no-js` class.

1. Add a `no-js` class added to the `html`
  ```
  <html class="no-js">
  ```

2. Add a script to remove the `no-js` class after confirming JS is available
  ```
  <script>
      // Confirm availability of JS and remove no-js class from html
      var docElement = document.documentElement;
      docElement.className = docElement.className.replace(/(^|\s)no-js(\s|$)/, '$1$2');
  </script>
  ```

3. Add the utility class to the element you want to hide
  ```
  <div class="u-js-only"></div>
  ```

#### Clearfix

Clear floated elements to avoid following elements from flowing into the previous one.


For example, to float an element to the left, but prevent the following text from flowing into it.

```
<div class="u-clearfix">
    <div style="float:left; width:100%; height:60px; background:black;"></div>
</div>
<em>This text would normally flow up into the black box if the box above</em>
```

_More information see: http://css-tricks.com/snippets/css/clear-fix/_

#### Visually hidden

Hide an element from view while keeping it accessible to screen readers.

For example, to create a link with a social network icon, but allow non-sighted users to understand the context, add descriptive text with the `u-visually-hidden` class.

```
<h1>
    <a href="#">
        <span class="cf-icon cf-icon-twitter-square"></span>
        <span class="u-visually-hidden">Share on Twitter</span>
    </a>
</h1>
```

#### Inline block

Add a .lt-ie8 class to hack inline-block for IE 7 and below.

```
<div class="u-inline-block"></div>
```

#### Float right

```
<div class="u-right"></div>
```

#### Break word

Force word breaks within an element. Useful for small containers where text may over-run the width of the container.

```
<div style="width: 100px;">
    This link should break:
    <br>
    <a class="u-break-word" href="#">
        something@something.com
    </a>
    <br>
    <br>
    This link should not:
    <br>
    <a href="#">
        something@something.com
    </a>
</div>
```

_This only works in IE8 when the element with the .u-break-word class has layout. See <http://stackoverflow.com/questions/3997223/word-wrapbreak-word-not-working-in-ie8> for more information._


### Mixins

#### Align with button

Align an element vertically with the text within a button that may be to either side.

```
.u-align-with-btn(@font-size: @base-font-size-px);
```

_Pass font-size as the argument for calculating spacing, default value is `@base-font-size-px`._

#### Felxible proportional containers

Utilize intrinsic ratios to create a flexible container that retains an aspect ratio. When image tags scale they retain their aspect ratio, but if you need a flexible video you will need to use this mixin.

_Read more about intrinsic rations: http://alistapart.com/article/creating-intrinsic-ratios-for-video_

```
.u-flexible-container-mixin(@width: 16, @height: 9);
```

In addition to the mixin, there are two default classes available for building 16:9 and 4:3 containers.

__NOTE: Inline background properties for demonstration only__

To create a 16:9 flexible video player, wrap the video element in an element with `u-flexible-container` and add the `u-flexible-container_inner` to the video element.

```
<div class="u-flexible-container">
    <video class="u-flexible-container_inner"
           style="background:#75787B;"
           controls>
    </video>
</div>
```

To create a flexible container with only a background (no inner video or object element), ommit the inner container.

```
<div class="u-flexible-container"
     style="background-image: url(http://placekitten.com/700/394);
            background-position: center center;
            background-repeat: no-repeat;"></div>
```

To create a 4:3 flexible video player, add the `__4_3` modifier to the container

```
<div class="u-flexible-container u-flexible-container__4-3">
    <video class="u-flexible-container_inner"
           style="background:#75787B;"
           controls>
    </video>
</div>
```

_When using the mixin, pass the width as the first argument, and the height as the second argument, default values are `16, 9`._

_Original mixin credit: https://gist.github.com/craigmdennis/6655047_

#### Link Modifiers

Modify link properties using the following mixins.

##### Link Colors

Calling the mixin without arguments will set the following states - default(pacific), :hover(pacific-50), :focus:(pacific), :visited teal, :active navy.

`u-link__colors()`

Passing a single argument into the mixin will set the color for the default, :visited, :hover, :focus, :active states.

`u-link__colors(@c)`

Passing two arguments into the mixin will set the color for the default, :visited, and :active states as the first argument, and :hover and :focus as the second argument.

`u-link__colors(@c, @h)`

Passing five arguments will set the color for the default, :visited, :hover, :focus, and :active states respectively.

`u-link__colors(@c, @v, @h, @f, @a)`

Passing ten arguments will set the text (default, :visited, :hover, :focus, and :active states in the first five arguments) and border colors (default, :visited, :hover, :focus, and :active states in the following five arguments) separately.

`u-link__colors(@c, @v, @h, @f, @a, @bc, @bv, @bh, @bf, @ba)`

__A base mixin of `u-link__colors-base()` exists, but please refrain from using this mixin directly in order to promote consistent naming throughout this project. If you need to set colors for all states of a link, use `.u-link__colors(@c, @v, @h, @f, @a)`.__

##### Link borders

Force the default bottom border on the default and :hover states.

`.u-link__border()`

Turn off the default bottom border on the default and :hover states.

`.u-link__no-border()`

Turn off the default bottom border on the default state but force a bottom border on the :hover state.

`.u-link__hover-border()`

##### Link children

Calling this mixin without arguments will set the default color for the hover state of a child within a link, without affecting the link itself.

`.u-link__hover-child()`

Passing a single argument into the mixin will set a custom color for the hover state of a child within a link, without affecting the link itself.

`.u-link__hover-child(@c)`

#### Margin Utilites
