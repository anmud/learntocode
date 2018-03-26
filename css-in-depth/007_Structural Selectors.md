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
* These strucrural selectors target elements on the page based on their relationships to other elements in the DOM.
* Updates dynamically if page updates.
* Reduced need for extra markup, classes and IDs  * CSS2 / IE8

### Example

```css
* { color: hsl(205, 87%, 50%); text-decoration: underline;}
```
Now all the text in each div is blue and underlined

![StructuralSelecrors1](./StructuralSelectors1.png)
![StructuralSelecrors2](./StructuralSelectors2.png)
![StructuralSelecrors3](./StructuralSelectors3.png)
![StructuralSelecrors4](./StructuralSelectors4.png)

* If we use a selector: `:first-of-type`, everything just turn blue (all the text in all the divs).

```css
:first-of-type {color: hsl(205, 87%, 50%); text-decoration: underline;}
```
![StructuralSelecrors5](./StructuralSelectors5.png)

It's happened because we've selected the first of everything. And the first of everything is the body. 

* If we use `:first-child` selector for the div of the body, we'll have only the first div blue.
```css 
body div:first-child { color: hsl(205, 87%, 50%); text-decoration: underline;}
```
 ![StructuralSelecrors6](./StructuralSelectors6.png)

* If we use the same selector `:first-child` without mentioning a div in the code, we'll have the blue text of the first child of every div. 
```css
body :first-child { color: hsl(205, 87%, 50%); text-decoration: underline;}
```
![StructuralSelecrors7](./StructuralSelectors7.png)

* If we do `:last-child`, it matches the last child of every div.
```css
body :last-child { color: hsl(205, 87%, 50%); text-decoration: underline;}
```
![StructuralSelecrors8](./StructuralSelectors8.png)

* If we do `:last-of-type` for the body, it'll match the elements in each div, which are last of ther's type in the div.
```css
body :last-of-type { color: hsl(205, 87%, 50%); text-decoration: underline;}
```
![StructuralSelecrors9](./StructuralSelectors9.png)