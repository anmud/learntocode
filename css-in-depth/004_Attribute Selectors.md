
Every html element can have a number of attributes. Some of them are valid, some of them are invalid. 

The `[attribute]` selector is used to select elements with a specified attribute.
The following example selects all `<a>` elements with a target attribute:

```css
a [target] {
	background-color: yellow;
}
```

The `[attribute="value"]` selector is used to select elements with a specified attribute and value.
The following example selects all `<a>` elements with a `target="_blank"` attribute:

```css
a[target="_blank"] { 
	background-color: yellow;
}
```

