# Media Queries

Media Queries are expressions we can add to our code that modify our website based on characteristics of the device that's being viewed on. 

While media queries can be used for a variety of things and in a number of ways, we are going to focus on what are called breakpoints, which are the viewport width at which we want our design to change. We then write the code inside that media query, with a set breakpoint, that we want to go into effect only when the viewport width that the app is being viewed on is at least the breakpoint width. Only the CSS that we want to change needs to go here - the original CSS rules will all still apply, and only the new CSS rules written inside the media query will override any pre-existing rules.

Key Term
viewport - the area of the window in which web content can be seen. We use the dimensions of the viewport (usually the width, but sometimes the height) as the basis of our media queries.

**For more information about viewport see**

- (What is a viewport?)[https://developer.mozilla.org/en-US/docs/Web/CSS/Viewport_concepts#What_is_a_viewport]
- (Using the viewport meta tag to control layout on mobile browsers)[https://developer.mozilla.org/en-US/docs/Mozilla/Mobile/Viewport_meta_tag]

## Adding Media Queries in Code

Media queries are used to set different style rules for different devices or sized screens. We use breakpoints to set the condition of a media query. The logic is:

```css
@media(feature:value)
```

Here media features are aspects of the device that our media (website) is being viewed on. The media feature we are most interested in for this lesson is width, which allows us to evaluate the viewport width of the browser and set conditions based on that evaluation. We actually write this feature min-width (or max-width) because width is one of many media features that are range features, which means they can be prefixed with min- or max- to express constraints, which is what we're looking for with our breakpoints! If the constraint of the breakpoint (viewport width being in the range below our breakpoint) is broken (the width is larger than the breakpoint) the new CSS rule takes effect. Here is an example of how that could look in action:

```css
@media(min-width:900px) {
  body{
   background:red;
 }
}
```

In this example if the viewport width is greater than 900px the background of the webpage would turn red.

Media queries are used to create responsive layouts using breakpoints. Below is an example of the syntax that is used for creating media queries:

```css
@media(min-width:1100px) {
  body{
    font-size: 27px;
  }
}
```

In the example above, if the browser width of the webpage being viewed is above 1100px wide, then the font-size would become 27px.

## Multiple Breakpoints

We have seen how to set a breakpoint and use Media Queries to create different layouts for smaller screens and larger screens, but there are some development moments that will call for 3 possible layouts.


A simple example would be creating 2 different breakpoints so that up to x width one set of CSS rules apply, then between x and y width a second set would apply, and then for anything beyond a width of y a third set of CSS rules would apply.


Here is an example of what that code could look like:

```css
/* Anything smaller than first breakpoint 600px */
.container {
  // rules for small screen
}

/* Medium Screens */
@media (min-width: 600px) and (max-width:900px) {
  .container {
    // rules for medium-sized screen
  }
}

/* Large Screens */
@media (min-width:901px) {
  .container {
    // rules for large screen
  }
}
```

In this example, the medium screens media query is new, and we use the keyword and to build a complex media query that evaluates both a min and max to create a range for the CSS rules to apply, in this case if the width of the viewport is between 600px-900px.

Complex media queries can be built using the keyword and to bound CSS rules between a range using min-width and max-width.

**Further Research**

Media Queries are actually a vast landscape of possibility, most of which you will probably never use - but, having a strong grasp of media queries and responsive breakpoints is essential for a web developer. For more information see the **MDN docs entry on using Media Queries.**