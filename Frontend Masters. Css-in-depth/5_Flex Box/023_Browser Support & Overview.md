# Flex Box Specification

CSS Flexible Box Layout Module Level 1

https://drafts.csswg.org/css-flexbox/ 


[Browser support](https://caniuse.com/#feat=flexbox)

### Example
Here we have an unordered list of navigational items:

![nav-items](../nav-items.png)

```css 
.ul {
  display: flex;
  padding: 3px;
  align-items: baseline;
  justify-content: center;
}

ul > li {
  text-align: center;
  flex: auto;
}
```
Or we can do 

```css
ul {
  display: flex;
 
}

ul > li {
  flex: auto;
}
```
![nav-items2](../nav-items2.png)

# Holy Grail Layout

![holy-grail-layout](..//holy-grail-layout.png)

```css

body {
  display: flex;
  flex-flow: column;
}
main {
  display: flex;
  flex: 1;
}
article {
  flex: 1;
}
nav {
  order: -1;
}
```


