An Html page has a certain structure

Structural Selectors are the following:
```css
:root

:empty

:blank

:nth-child()

:nth-last-child()

:first-child*

:last-child

:only-child

:nth-of-type()

:nth-last-of-type()

:first-of-type

:last-of-type

:only-of-type
```
* These strucrural pseudo classes target elements on the page based on their relationships to other elements in the DOM.
* Updates dynamically if page updates.
* Reduced need for extra markup, classes and IDs  * CSS2 / IE8

### Example

```css
* { color: hsl(205, 87%, 50%); text-decoration: underline;}
```
Now all the text in each div is blue and underlined

![StructuralSelectors1](./StructuralSelectors1.png)
![StructuralSelectors2](./StructuralSelectors2.png)
![StructuralSelectors3](./StructuralSelectors3.png)
![StructuralSelectors4](./StructuralSelectors4.png)

* If we use a pseudo class `:first-of-type`, everything just turn blue (all the text in all the divs).

```css
:first-of-type {color: hsl(205, 87%, 50%); text-decoration: underline;}
```
![StructuralSelectors5](./StructuralSelectors5.png)

It's happened because we've selected the first of everything. And the first of everything is the body. 

* If we use `:first-child` pseudo class for the div of the body, we'll have only the first div blue.
```css 
body div:first-child { color: hsl(205, 87%, 50%); text-decoration: underline;}
```
 ![StructuralSelectors6](./StructuralSelectors6.png)

* If we use the same pseudo class selector `:first-child` without mentioning a div in the code, we'll have the blue text of the first child of every div. 
```css
body :first-child { color: hsl(205, 87%, 50%); text-decoration: underline;}
```
![StructuralSelectors7](./StructuralSelectors7.png)

* If we do `:last-child`, it matches the last child of every div.
```css
body :last-child { color: hsl(205, 87%, 50%); text-decoration: underline;}
```
![StructuralSelectors8](./StructuralSelectors8.png)

* If we do `:last-of-type` for the body, it'll match the elements in each div, which are last of ther's type within that div.
```css
body :last-of-type { color: hsl(205, 87%, 50%); text-decoration: underline;}
```
![StructuralSelectors9](./StructuralSelectors9.png)

* if we do `:last-child`, it'll match the last child in each div.

![StructuralSelectors10](./StructuralSelectors10.png)

The difference between `:last-child` and `:last-of-type`: it doesn't matter how many elements there are in the div - `:last-of-type` pseudo class will match every element that is last of it's type. The `:last-child` selector will match only one last element of the div, and it doesn't matter of what type it is. The thing is, this doesn't match classes. 

If we do  
```css
li.foo :last-child 
```
This way - if a last element doesn't have a class of `.foo`, it won't match. 

If we do  
```css
li.foo :last-of-type
```
This way - it will be any element with the class of `.foo` based on it's type in a div.  

* If we do `:only-of-type`, it'll mach only one of that type. 

```css
body :only-of-type { color: hsl(205, 87%, 50%); text-decoration: underline;}
```
![StructuralSelectors11](./StructuralSelectors11.png)
![StructuralSelectors12](./StructuralSelectors12.png)

* If we do `:only-child`, it'll match only the last div, cos it have only the child

```css
body :only-child { color: hsl(205, 87%, 50%); text-decoration: underline;}
```
![StructuralSelectors13](./StructuralSelectors13.png)

## There are several nth pseudo-classes.

It will help you to be more specific. nth pseudo-classes target element or elements based on argument passed to the selector. 

```css
:nth-child(3n)

:nth-last-child(odd)

:nth-of-type(5)

:nth-last-of-type(3n+1) 
```
n - is an interval

### Example 1

```css
li:first-child,
li:last-child {
  font-weight: bold;
}
li:first-of-type,
li:last-of-type{
  text-decoration:line-through;
}
li:nth-child(even) {
  background-color: #CCC;
}
li:nth-child(3) {
  color: #CCC;
}
li:nth-of-type(odd) {
  background-color: #FFF;
}
li:nth-of-type(4n) {
  color: hsl(205, 87%, 50%);
}
li:nth-of-type(3n-1) {
    text-align:right;
}

```

![nthpseudoclass](./nthpseudoclass.png)

### Example 2

```css
tr:nth-of-type(even) td:nth-of-type(even),
tr:nth-of-type(odd) td:nth-of-type(odd) {
	background-color: #900; color: #fff;
}
``` 
![nth-of-type](./nth-of-type.png)

