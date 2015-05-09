CSS Flexbox Essentials
==========

> Learning CSS Flexbox with Tuts Plus [course](http://webdesign.tutsplus.com/courses/css-flexbox-essentials).

## What is CSS Flexbox?

CSS layout model that makes it very easy to layout content without having to rely on floats and inline block elements.

Supports laying out rows and columns that are automatically responsive.

Makes it easy to re-arrange content depending on browser size, including order of content.

[W3C Spec](http://www.w3.org/TR/css-flexbox-1/) | [Can I Use](http://caniuse.com/#feat=flexbox)

## Flexbox Containers

[HTML](site01/index.html) | [CSS](site01/styles.css)

By default, `div` is block level element, arranged vertically.
Unlike `inline` elements which are arranged horizontally, or side by side.

A `flex` element can be arranged vertically _or_ horizontally.

If set a `div` element to `display: inline`, then no longer have control over the with and height.
`display: inline-blcok` will both lay out horizontally and allow for control of width and height,
but flexbox will provide a lot more flexibility.

To get started with flexbox, set the parent element's display property to `flex`, for example

```css
.container {
  background-color: #555;
  width: 800px;
  height: 400px;
  margin: 0 auto;
  display: flex;
}
```

By default, all items in container will be arranged horizontally, _and_ taking up full height of the container.
And this holds without having to set any display property (inline, inline-block, etc.) on the children elements.
