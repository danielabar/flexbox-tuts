<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](http://doctoc.herokuapp.com/)*

- [CSS Flexbox Essentials](#css-flexbox-essentials)
  - [What is CSS Flexbox?](#what-is-css-flexbox)
  - [Flexbox Containers](#flexbox-containers)
  - [Column Widths](#column-widths)
  - [Width Shorthand](#width-shorthand)
  - [Flex Direction](#flex-direction)
  - [Re-ordering Content](#re-ordering-content)
  - [Adding Content](#adding-content)
  - [Content Spacing](#content-spacing)
  - [Wrapping Content](#wrapping-content)
  - [Flex-Flow Shorthand](#flex-flow-shorthand)
    - [Column Wrap Issues](#column-wrap-issues)
  - [Cross-Axis Alignment](#cross-axis-alignment)
    - [Columns](#columns)
    - [Rows](#rows)
  - [Justifying Content](#justifying-content)
  - [Align Items](#align-items)
  - [Adding Vendor Prefixes](#adding-vendor-prefixes)
  - [Building a simple layout](#building-a-simple-layout)
  - [Styling the layout](#styling-the-layout)
  - [Finishing the styles](#finishing-the-styles)

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

## Width Shorthand

[HTML](site03/index.html) | [CSS](site03/styles.css)

`flex` property is a shorthand that accepts three values:

* flex-grow value
* flex-shrink value
* flex-basis value

For example:

```css
.item {
  flex: 1 1 150px;
}
```

Even shorter, this will make this item always be twice as wide as its siblings, if they have `flex: 1`

```css
.item {
  flex 2;
}
```

In this shorthand style, the flex-basis is not specified, therefore will be determined by the content in the div.

## Flex Direction

[HTML](site04/index.html) | [CSS](site04/styles.css)

`flex-direction` property is used to specify whether to create columns or rows.
This property must be applied to the container. Tells that container _how_ to layout the items within that container.

Values can be `row` (default), which will arrange items horizontally, i.e. beside each other.

`column` will arrange items vertically, i.e. stacked one underneath the other.

Note that when flex-direction is set to column, height of items within container is distributed in the same way width is when using row, i.e. uses flex-grow and flex-shrink.

Another value of flex-direction is `row-reverse`, lays out items horizontally, but in reverse order from what they appear in dom.

`column-reverse` lays out items vertically, in reverse order.

## Re-ordering Content

[HTML](site05/index.html) | [CSS](site05/styles.css)

`order` property can be applied to items within the flex container, and items will be ordered according to that value.

Order values don't need to be sequential or match the number of items in the container.
Will simply order from smallest to largest value.

Will order rows or columns, depending on value of `flex-direction` applied to container.

The `order` property is useful if you want to re-order content based on browser width.
For example, suppose container has `max-width: 800px` and want order of divs to change when browser is 600px wide or less,
this can be accomplished with media query that changes order:

```css
@media (max-width: 600px) {
  .item1 { order: 100; }
  .item2 { order: 1; }
  .item3 { order: 1; }
  .item4 { order: 1; }
}
```

## Adding Content

[HTML](site06/index.html) | [CSS](site06/styles.css)

Challenge with columns having varying amounts of text is getting the height right.

Flexbox supports columns with varying amounts of text and will make them all the same height.

## Content Spacing

[HTML](site07/index.html) | [CSS](site07/styles.css)

Use combination of padding and margin on columns.

## Wrapping Content

[HTML](site08/index.html) | [CSS](site08/styles.css)

As browser window gets smaller in width, columns keep shrinking in width until it gets hard to read.

One solution is to set `min-width` on columns, but their container still shrinks, and this creates a horizontal scroll.

A better solution is to get some columns to wrap to the next line at a certain width.
This can be achieved using `flex-wrap` property, which by default, is set to `nowrap`.
This property is applied to the container. For example:

```css
.container {
  background-color: #555;
  max-width: 800px;
  margin: 0 auto;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
}

.item {
  background-color: #f9f9f9;
  color: #333;
  font-weight: 400;
  padding: 10px;
  margin: 10px;
  min-width: 150px;
}
```

As the browser width shrinks, when items can no longer be `min-width` wide, they get wrapped to the next "row",
starting with last item, then second last etc. (unless there's a media query in effect that changes order).

`flex-wrap: wrap-reverse` has similar effect as `wrap` but reverses order, so first item gets wrapped first.

## Flex-Flow Shorthand

[HTML](site09/index.html) | [CSS](site09/styles.css)

To recap, there are two properties that handle flow, `flex-direction` which handles direction of flow (horizontal or vertial)
and `flex-wrap`, which affects how items behave when they become too big for container.

`flex-flow` is a shorthand property that ties these two together.
First value is flex-direction and second is flex-flow. For example:

```css
.container {
  background-color: #555;
  max-width: 800px;
  margin: 0 auto;
  display: flex;
  flex-flow: row wrap;
}
```

### Column Wrap Issues

Note that if flex-flow is set to `column wrap`, won't see any wrapping effect unless a height is set on the container.

However, with a height set, column content will overflow. To fix this, set `flex-basis` on each item to `auto`.

After fixing that, next problem will be that content takes up 100% of width so when wraps to next column,
it goes off the screen width.

To fix this, remove `min-width` from items and instead set a small-ish `width`.
And also set `min-height` on each item.

## Cross-Axis Alignment

[HTML](site10/index.html) | [CSS](site10/styles.css)

### Columns

In previous exercise where columns were wrapped, there is a big gap between the columns.
Because the items have fixed width of 200 set, flexbox is trying to space them out evenly.

`align-content` property can be used to adjust the extra space between columns, i.e. horizontal cross axis.

Alignment properties try to adjust positioning of items within the container when there is space left over,
i.e. will see the effect when the items have a hard-coded width (columns) or height (rows),
because if there is no hard-coded width or height, then there's never any space left over.

This property is applied to the container. For example, to align to the start of the cross axis:

```css
.container {
  background-color: #555;
  height: 700px;
  margin: 0 auto;
  display: flex;
  flex-flow: column wrap;
  align-content: flex-start;
}
```

Setting `align-content: center` will keep columns next to each other, but centered within the container.

`flex-end` will align all the content to the right side of container.

`space-around` will put even spacing around both sides of each column.

`space-between` gets even space between the columns, but doesn't deal with space at left and right ends.

`stretch` is the default value, which tries to adjust width of items, but if the items have a hard coded width,
will simply space things out.

### Rows

When dealing with rows, the main axis is horizontal, therefore the cross-axis is vertical.

If `flex-flow` is set to `row wrap`, then `align-content` affects the up and down cross axis (i.e. vertical alignment).

## Justifying Content

[HTML](site11/index.html) | [CSS](site11/styles.css)

This is the opposite of align-content in that it deals with the _main_ axis rather than the _cross axis_..

When dealing with rows, the main axis is horizontal. `justify-content` property is applied to the container.
For example, to center rows horizontally:

```css
.container {
  background-color: #555;
  height: 700px;
  margin: 0 auto;
  display: flex;
  flex-flow: row wrap;
  justify-content: center;
}
```

`justify-content` can be set to the same values as `align-content` (flex-start, flex-end, space-around, etc).

## Align Items

[HTML](site12/index.html) | [CSS](site12/styles.css)

`align-items` is a property to align items vertically in the container based on the height of the items.
Default value is `stretch`, which makes items fill the entire height of the container if they don't have an
explicit height set.

`align-items` is set on the container, for example:

```css
.container {
  background-color: #ddd;
  min-height: 400px;
  width: 800px;
  margin: 0 auto;
  display: flex;
  flex-flow: row wrap;
  align-items: flex-start;
}
```

`flex-start` will lets items retain their natural height based on how much content is inside each item.
This property also aligns top edge of the items with the top edge of the container.

'flex-end' aligns the bottom edges of the items with the bottom edge of the container,
i.e. moves all the items to the bottom of the container.

When dealing with rows, main axis is horizontal (left to right), therefore `align-items` aligns items on the cross axis,
i.e vertical axis, while retaining their natural height.

`center` will vertically center the items.

`baseline` at first appears to have same effect as `flex-start`, but if item's content is in different places due to a variety of margin and padding, then `baseline` will vertically align the start of the text in each item to each other.
i.e. `baseline` adjusts for margin and padding.

`align-self` property can be applied to an individual item within the flex container, for example:

```css
.item1 {
  padding-top: 20px;
  width: 150px;
  align-self: flex-end;
}
```

This will make item1 ignore the `align-items` property st on the container and apply its own alignment instead.

In summary `align-items` allows for vertical alignment of items within a container,
without requiring that they stretch to the full height of the container.

## Adding Vendor Prefixes

[HTML](site13/index.html) | [CSS](site13/styles.css)

Install Autoprefixer plugin in your editor of choice to generate vendor prefixed css.
Otherwise for example, it doesn't render properly in Safari.

For example, running Autoprefixer on flex container generates:

```css
.container {
  background-color: #ddd;
  min-height: 400px;
  width: 800px;
  margin: 0 auto;
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  -webkit-flex-flow: row wrap;
      -ms-flex-flow: row wrap;
          flex-flow: row wrap;
  -webkit-box-align: baseline;
  -webkit-align-items: baseline;
      -ms-flex-align: baseline;
          align-items: baseline;
}
```

## Building a simple layout

[HTML](site14/index.html) | [CSS](site14/styles.css)

Start with unstyled html to get the content in place.

## Styling the layout

[HTML](site15/index.html) | [CSS](site15/styles.css)

## Finishing the styles

[HTML](site16/index.html) | [CSS](site16/styles.css)
