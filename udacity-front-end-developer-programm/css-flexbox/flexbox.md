# CSS Flexbox

To use `flexbox` set the display property of a `div` to `flex`. The items inside that element will automatically become `flex` items, and you can then use the `flexbox syntax` in your CSS code.

By setting an element's display property to `flex`, all elements inside of it become `flex items` that can be laid out in a customized way following design patterns like `columns`, `rows`, `alignment`, and `distribution`.

Here, we have learned that Flexbox (the Flexible Box Module) is a set of CSS rules for stretching multiple columns or rows across a parent container. Flex is unique amongst CSS properties because you have a main container and the items nested within it. CSS flex has properties that apply to both the element itself, and the items inside of it.

To use flexbox set the display property of the parent container to flex:

```css
.container{
  display:flex;
}
```

## Axes and Direction with Flexbox

The Flexbox model relies on two axes: the main axis and the cross axis. The main axis is defined by flex-direction, which has four possible values:

- row
- row-reverse
- column
- column-reverse

The two row settings will create the main axis horizontally - or inline direction. The two column settings will create the main axis vertically - or block direction. block or inline here refer to the CSS display settings which we have covered previously.

The axis determines the flow of your content - you can think of this as being either rows or columns - and they will be determined when you start aligning and justifying content within a flex container.

## Axes and Direction in Action

After setting an element's display to flex, the next thing you will usually want to state is whether the elements inside the container should be laid out in rows or columns. You can do this using the `flex-direction` property, and setting its value to either `column` or `row`.

To set the layout of the items in a flex container to either a row or column use the flex-direction property like this:

```css
.container{
  display:flex;
  flex-direction: row
}
```

- If the flex-direction is set to row or row-reverse the main axis is horizontal.

- If the flex-direction is set to column or column-reverse the main axis is vertical.

- If the main axis is horizontal the cross axis is vertical.

- The two axis control the flow of space in flexbox and correspond to the align-items and justify-content properties.

`Axes` and `direction` are important concepts for understanding `flexbox`. They are both conceptual and technical which can be tricky. One suggestion is to try and draw your flex containers out first in a notebook. This can be helpful for mapping out axes and direction.

## Ordering Elements with Flexbox

There are three ways to explicitly set the order in which items will appear in a grid.

1. Moving the HTML code for the elements themselves to reorder
2. Appending `-reverse` to `row` or `column` will reverse the order in the specified `row` or `column`
3. Using the `order` property of the individual items inside the grid

The `order` CSS property is cpecifically for Flex items. That is HTML elements that are inside of another HTML element that has the display Flex. That's the Flex container inside it are the flex items. Flex items have a CSS property called `order`, tha can set the order that they can appear in your browser. 

## Aligning Items and Justyfying Content with Flexbox

To align items on the cross axis use align-items with the possible values:

- stretch
- flex-start
- flex-end
- center

To justify content on the main axis use justify-content, which has the possible values:

- flex-start
- flex-end
- center
- space-around
- space-between
- space-evenly

