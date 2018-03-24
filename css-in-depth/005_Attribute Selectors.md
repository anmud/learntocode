
**Every `html` element can have a number of attributes. Some of them are valid, some of them are invalid.**

* The `[attribute]` selector is used to select elements with a specified attribute.
The following example selects all `<a>` elements with a target attribute:

**CSS Snippet**
```css
a [target] {
	background-color: yellow;
}
```

* The `[attribute="value"]` selector is used to select elements with a specified attribute and value.
The following example selects all `<a>` elements with a `target="_blank"` attribute:

**CSS Snippet**
```css
a[target="_blank"] { 
	background-color: yellow;
}
```

* The `E[attr|=val]` selector is uded to selects elements whose attribute has a value or begins with val- ("val" plus "-").
**CSS Snippet**
```css
p[lang|="en"]{
	/* <p lang="en-us">  <p lang="en-uk"> */ 
	}
	```

* The `[attribute~="value"]` selector is used to select elements with an attribute value containing a specified word.
The following example selects all elements with a title attribute that contains a space-separated list of words, one of which is "flower":
**CSS Snippet**
```css
[title~="flower"] {
	border: 5px solid yellow;
}
```
**Level 3 Attribute Selectors**

* `The E[attr^=val]` selector is used to select elements whose attribute starts with the value.
**CSS Snippet**
```css
a[href^=mailto] {
	background-image: url(emailicon.gif);
	}
	```
```css
a[href^=http]:after {
	content: " (" attr(href) ")";
	}
	```
* The `E[attr$=val]` selector is used to select elements whose attribute ends in value. 
**CSS Snippet**
```css
a[href$=pdf] {
	background-image: url(pdficon.gif);
	}
	```
```css
a[href$=pdf]:after {
	content: " (PDF)";
	}
	```

* The `E[attr*=val]` selector is used to select elements with the val that’s anywhere in the content.

**For Styling Forms**

The attribute selectors can be useful for styling forms without class or ID:

Example:
**CSS Snippet**
```css
input[type="text"] {
	width: 150px;
	display: block;
	margin-bottom: 10px;
	background-color: yellow;
}
```

```css
input[type="button"] {
	width: 120px;
	margin-left: 35px;
	display: block;
}
```
**Case Insensitivity**






