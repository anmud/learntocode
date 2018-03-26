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
![StructuralSelecrors1](./StructuralSelectors1.png)
![StructuralSelecrors2](./StructuralSelectors2.png)
![StructuralSelecrors3](./StructuralSelectors3.png)
![StructuralSelecrors4](./StructuralSelectors4.png)

If we use a selector: `:first-of-type`, everything just turn blue.

```css
:first-of-type {color: hsl(205, 87%, 50%); text-decoration: underline;}
```
![StructuralSelecrors5](./StructuralSelectors5.png)

It's happened because we've selected the first of everything. And the first of everything is the body. 

If we use `:first-child` selector for the body, we'll have only the first part blue.
```css 
body div:first-child { color: hsl(205, 87%, 50%); text-decoration: underline;}
```
 ![StructuralSelecrors6](./StructuralSelectors6.png)