
**A CSS pseudo-element is used to style specified parts of an element.**

For example, it can be used to:

* Style the first letter, or line, of an element
* Insert content before, or after, the content of an element

```
::first-line
::first-letter
::selection (not in specification)
::before
::after
```

Pseudo-classes select elements that already exist.
Pseudo-elements create "faux" elements you can style.

* `::first-letter` pseudo-element
The ::first-letter pseudo-element is used to add a special style to the first letter of a text.

```css
p:first-of-type::first-letter {
	position: relative;
	top: 8px;
	float: left;
	font-size: 3em;
	line-height: 1;
	color: hsl(205, 87%, 50%);
	padding: 0 4px 2px 0;
	font-weight: bold;
}
```
![firstletterPseudoElement](./firstletterPseudoElement.png)

* `::selection` pseudo-element

The ::selection pseudo-element matches the portion of an element that is selected by a user.
The following CSS properties can be applied to ::selection: color, background, cursor, and outline.

**CSS**
```css
::selection {
    color: red; 
    background: yellow;
}
```
**HTML**
```html
<!DOCTYPE html>
<html>
<head>
<style>
::-moz-selection { /* Code for Firefox */
    color: red;
    background: yellow;
}

::selection {
    color: red;
    background: yellow;
}
</style>
</head>
<body>

<h1>Select some text on this page:</h1>

<p>This is a paragraph.</p>
<div>This is some text in a div element.</div>

<p><strong>Note:</strong> ::selection is not supported in Internet Explorer 8 and earlier versions.</p>
<p><strong>Note:</strong> Firefox supports an alternative, the ::-moz-selection property.</p>

</body>
</html>
```
![selectionPseudoElement](./selectionPseudoelement.png)

