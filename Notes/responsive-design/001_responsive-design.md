# Responsive Design

## The Ingredients

There are three core ingredients:

- a flexible, grid-based layout,
- flexible images and media
- media queries, a module from the CSS3 specification

### The Flexible Grid

Our canvas, the browser window, can bend and flex to any shape or size. Often the first layer of our grid-based layouts looks like this:

```css
.page{
    width: 960px;
    margin: auto;
}
```

We create an element in our markup, give it a fixed width in our CSS, and center it in the page. But when we are thinking flexibly, we need to transform it into something more fluid, something more propotional. 
How do we begin?

#### Flexible Typesetting

```html
<h1>Achieve sentense with Skynet! <a href='#'>Read more &raquo;</a></h1>
```

A headline with a link embedded in it - a fine foundation of `semantic markup`. With our foundation in place, we can begin adding a layer of `style`. Let's start by applying some basic rules to the `body` element. 

```css
body{
    background-color: #DCDBD9;
    color: #2C2C2C;
    font: normal 100% Cambria, Georgia, serif;
}
```

> The `font-size` has been set to **100%**. In doing so, we've simply set our `base type size` to the **browser's default**, which is in most cases **16 pixels**. We can then use **ems** to size text up or down to the related baseline. 

At any rate, our `h1` looks too small: it's inheriting the `font-size` of `100%` we set on the `body element`, and rendering at the `browser's default type size` of `16 pixels`. For the purpose of our typesetting experiment, let's start to think proportionally, and express pixel based `font-size values` in relative terms. So, instead of `pixels` we'll use the **em**.  

```css

h1{
    font-size: 1.5 em;
    font-style: italic;
    font-weight: normal;
}

h1 a{
    color: #747474;
    font: bold 0.458333333333333em Calibti, Optima, Arial, sans-serif;
    letter-spacing: 0.15em;
    text-transform: uppercase;
    text-decoration: none;
```

#### Contextual healing

To do so, we need a bit of math: we'll take the `*target*` font-size and devide it by the font-size of its `containing element`. The result will be our desired font-size expressed with flexible **ems**. 

In other words, `relative type sizes` can be calculated with this simple formula:

`target / context = result `

So, what's then with our `h1`? Assuming that our base font-size: 100% on the body element equates to 16 pixels, we can express out `h1's` target font-size (24px) relative to its context (16px), so we get:

`24 / 16 = 1.5 `

And there we are: 24px is 1.5 times grater than 16px, so our `font-size` is **1.5 em**.

Let's continue with our `read more` link. Note that it also inherits the font-size: 1.5em set on its containing element, the `h1`. **Important** here is that all `elements` inside the `headline` need to be expressed in relation to that value. In other words *our context has changed*. 

So, to set the `font-size` of our `link` in **ems**, we'll devide our target of 11 px by 24px - the font-size of the headline, our new context. 

`11 / 24 = 0.458333333333333`

> Note, we won't round this number! Actually, it petfectly represents our desired font-size in proportional terms. 


#### From flexible fonts to flexible grid

Every aspect of our **grid** - the `rows` and `columns`, and the `modules` draped over them - can be expressed as *proportions* of their `containing element`.

Let's say we have `basic markup structure`. 

```html
<div class='page'>
  <div class='blog section'>

     <h1 class='lede'>Recently in <a href='#'>The Bot Blog</a></h1>

     <div class='main'>
     ...
     </div><!--/end .main-->
     
      <div class='other'>
     ...
     </div><!--/end .other-->

  
  </div><!--/end .blog section-->
</div><!--/end .page-->
```

![blog-grid](./blog-grid.png)

We’ve created a `generic container` for the entire `page` (*.page*), which in turn contains our `.blog module`. And within `.blog` we’ve created two more `containers`: a `div` classed as `.main` for our main `article content`, and another `div` classed as `.other` for, um, other stuff. 

