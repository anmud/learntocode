# Syntax

```css
element::before {
  /* the only 'required' attribute */
  content: ""; 
 }

element::after {
  /* without "content:", you have no content */
  content: ""; 
 }
 ``` 

## Values for content 

* **none** - same as no content property declared
* **normal** - default value. Sets the content, if specified, to normal, which default is "none" (which is nothing)
* **string** - sets the content to the text you specify. a string of text, can be combined with URL, counter, attr(X), quotes, etc.
* **image** - url of a resource, usual an image
* **counter** - sets the content as a counter. counter(name), counter(name,style), counter(name, string) or counters(name,string,style); 'name' is a string,but not 'none', 'inherit' or 'initial'
* **open-quote/close quote** - sets the content to be an opening/closing quote 
* **no open-quote/ no close quote** - removes the opening/closing quote from the content, if specified 
* **attr(X)** - displays the value of the attribute 'X'
* **inherit** - inherits this property from its parent element.

### Example

"My name is Donald"

"I live in Ducksburg"

"Note: You cannot have "close-quote" without "open-quote"."

**HTML**
```html
<!DOCTYPE html>
<html>
<head>
</head>
<body>

<p>My name is Donald</p>
<p>I live in Ducksburg</p>

<p><b>Note:</b> You cannot have "close-quote" without "open-quote".</p>

</body>
</html>
```
**CSS**
```css
p::before {
    content: open-quote;
}

p::after {
    content: close-quote;
}
```