# Counters

Counters let you adjust the appearance of content based on its placement in the document.
CSS counters are like "variables". The variable values can be incremented by CSS rules (which will track how many times they are used).

To work with CSS counters we will use the following properties:

* counter-reset - Creates or resets a counter
* counter-increment - Increments a counter value
* content - Inserts generated content
* counter() or counters() function - Adds the value of a counter to an element

To use a CSS counter, it must first be created with counter-reset.

The following example creates a counter for the page (in the body selector), then increments the counter value for each <h2> element and adds "Section <value of the counter>:" to the beginning of each <h2> element:

**HTML**
```html
<!DOCTYPE html>
<html>
<head>
</head>
<body>

<h1>Using CSS Counters:</h1>
<h2>HTML Tutorial</h2>
<h2>CSS Tutorial</h2>
<h2>JavaScript Tutorial</h2>

<p><b>Note:</b> IE8 supports these properties only if a !DOCTYPE is specified.</p>

</body>
</html>
```
**CSS**
```css
body {
    counter-reset: section;
}

h2::before {
    counter-increment: section;
    content: "paragraph " counter(section) ": ";
}
```
Using CSS Counters:
paragraph 1: HTML Tutorial
paragraph 2:CSS Tutorial
paragraph 3:JavaScript Tutorial

**Note:** IE8 supports these properties only if a !DOCTYPE is specified.

## attr() support, or lack thereof
Html elements can have any number of attributes. and when we do attributhe with the attribute name on an element, it will print the value. If it prints the value of the string, it will not interpolate the value of that string. 
If we put the image, it will give us just the url of the image, not actually put the image. 

Supported

`attr( attrName )`

Not yet

* `attr( attrName unit? [ , fallback ]? )`
* any use outside of content:
`string` `color` `url` `integer` `number` `length`, `angle`, `time or frequency` `length or unit token`

in the future we'll have: 

```<p data-count="5">Hi</p>

width: attr(data-count em, auto);
```
