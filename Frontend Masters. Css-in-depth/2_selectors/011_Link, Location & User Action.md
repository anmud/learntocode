# Link pseudo classes

`<a>` with an `href` attribute

```
:link
:visited
```
CSS Selectors Level 4

```
:any-link
```
<pre><code><del>
:local-link</del>
<del>:local-link(n)</del></pre></code>

`:any-link` is the same as :`matches(:link, :visited)`

# User Action pseudo classes 


```
:hover
:active
:focus
```

```
:focus-ring
:focus-within
:drop
:drop()
```
**Note:** always style `:focus` when you style `:hover`; `:focus` and `:active` at the same time. 

```css
a:visited:hover
button:active:focus
```
**Note** NEVER do `*:focus { outline: none; }`

# Drag & Drop pseudo classes 

* `:drop`
drop targets while the user is “dragging”.
Unfortunately, dropzone attribute is not yet supported
* `:drop(active)`
current drop target for the drag operation.
* `:drop(valid)`
drop target is valid for the object currently being dragged, like correct filetype.
* `:drop(invalid)`
drop target is invalid for the object currently being dragged, i.e. doesn't except the 

# Other pseudo classes

**`:target` pseudoclass**

The `:target` CSS pseudo-class represents a unique element (the target element) with an id matching the URL's fragment.

```css
/* Selects an element with an ID matching the current URL's fragment */
:target {
  border: 2px solid black;
}
```
For example, the following URL has a fragment (denoted by the # sign) that points to an element called section2:

http://www.example.com/index.html#section2

The following element would be selected by a `:target` selector when the current URL is equal to the above:

```html
<section id="section2">Example</section>
```
### Examples

**A table of contents**

The `:target` pseudo-class can be used to highlight the portion of a page that has been linked to from a table of contents.

**HTML**

```html
<h3>Table of Contents</h3>
<ol>
 <li><a href="#p1">Jump to the first paragraph!</a></li>
 <li><a href="#p2">Jump to the second paragraph!</a></li>
 <li><a href="#nowhere">This link goes nowhere,
   because the target doesn't exist.</a></li>
</ol>

<h3>My Fun Article</h3>
<p id="p1">You can target <i>this paragraph</i> using a
  URL fragment. Click on the link above to try out!</p>
<p id="p2">This is <i>another paragraph</i>, also accessible
  from the links above. Isn't that delightful?</p>
  ```
**CSS**

```css
p:target {
  background-color: gold;
}

/* Add a pseudo-element inside the target element */
p:target::before {
  font: 70% sans-serif;
  content: "►";
  color: limegreen;
  margin-right: .25em;
}

/* Style italic elements within the target element */
p:target i {
  color: red;
}
```
![targetPseudoClass](./targetPseudoClass.png)

**`:scope` pseudoclass**

This pseudo-class is called scope pseudo-class and represents any element that is in the contextual reference element set and if the contextual reference element set is empty `:scope` is equivalent to `:root`.

# Grid-stuctural selectors

**Column combinator** 

`E || F`

```css
col.selected || td {
  /* matches all cells within the column's scope*/
}
```

```
:nth-column(An+B)
:nth-last-column(An+B)
```
## Time dimensional

```
:current
:future
:past
```
## Video & Audio

```
:playing
:paused
```





