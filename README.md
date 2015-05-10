<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](http://doctoc.herokuapp.com/)*

- [CSS Flexbox Essentials](#css-flexbox-essentials)
  - [What is CSS Flexbox?](#what-is-css-flexbox)
  - [Flexbox Containers](#flexbox-containers)
  - [Column Widths](#column-widths)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

CSS Flexbox Essentials
==========

> Learning CSS Flexbox with Tuts Plus [course](http://webdesign.tutsplus.com/courses/css-flexbox-essentials).

## What is CSS Flexbox?

[W3C Spec](http://www.w3.org/TR/css-flexbox-1/) | [Can I Use](http://caniuse.com/#feat=flexbox)

CSS layout model that makes it very easy to layout content without having to rely on floats and inline block elements.

Supports laying out rows and columns that are automatically responsive.

Makes it easy to re-arrange content depending on browser size, including order of content.

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

The width of the elements will be just big enough to hold the content.

## Column Widths

[HTML](site02/index.html) | [CSS](site02/styles.css)

`flex-basis` is used to set the "natural" width.

`flex-grow` is used to compare its value against its sibling elements. The actual value is completely arbitrary.
`flex-grow` and `flex-shrink` properties adjust the widths of all of the items in the flex container
so that they take up as much room as possible in the container.

Value of `flex-grow` determines how much that particular item will grow in relation to its sibling elements.

However, setting one sibling `flex-grow` to 2 and the others to 1 does not necessarily mean one sibling will be twice as wide. Because `flex-grow` interacts with `flex-basis`, and will only grow by whatever room is left over.

For example, given a container width of 800px and 4 sibling div's with `flex-basis` of 150px (i.e. natural width):

If they all have `flex-grow` of 1, then after natural width is applied (150 * 4 = 600), that leaves 200px left over.
So each one would "grow" by 200 / 4 = 50px.

However, if one div has `flex-grow` of 2, then given the leftover 200px, that div will grow by twice as much as its siblings.
In this example, computed width = 250px (i.e. grow by 100 from its natural width).

`flex-shrink` property used to determine by how much the width should "shrink" if the div's are too wide to fit in the container.
For example, a container widht of 800px with 4 children div's of `flex-basis` 400px each.

If one of the child div's has a larger value of `flex-shrink`, for example 2, where all the other siblings have a value of 1,
then this child div will shrink twice as much as the rest of its siblings.

Both `flex-grow` and `flex-shrink` properties can be applied to the same element. Then depending on the container size,
the flexbox layout model will determine whether it needs to apply the grow or shrink properties.