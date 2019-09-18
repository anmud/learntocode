# Responsive Design

## The Ingredients

There are three core ingredients:

- a flexible, grid-based layout,
- flexible images and media
- media queries, a module from the CSS3 specification

## The Flexible Grid

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

We’ve created a `generic container` for the entire `page` (*.page*), which in turn contains our `.blog module`. And within `.blog` we’ve created two more `containers`: a `div` classed as `.main` for our main `article content`, and another `div` classed as `.other` for other stuff. 

So how exactly do we turn those `.main` and `.other` blocks into proper columns? Reviewing the design tells us a few things: first, that the `grid` itself is divided into `12 columns`, each measuring `69 pixels` across and separated by regular `12px-wide gutters`. Taken together, those columns and gutters give us a `total width` of `960 pixels`. However, the `blog` itself is only `900 pixels` wide, centered horizontally within that `960px-wide canvas`.

![grid-dimensions](./grid-dimensions.png)


So those are the high-level details. And if we take a closer look at the two columns inside of the `blog`, we can see that the `left-hand content column` (**.main** in our markup) is `566 pixels` wide, while the `right-hand`, secondary column (**.other**) is only `331 pixels` across.

![grid-narrow-focus](./grid-narrow-focus.png)

So, our css code will look like 

```css
.page {
 margin: 36px auto;
 width: 960px;
}
.blog {
 margin: 0 auto 53px;
 width: 900px;
}
.blog .main {
 float: left;
 width: 566px;
}
.blog .other {
 float: right;
 width: 331px;
}
```

we’ve set the width of **.page** to `960` pixels, centered the 900px-wide **.blog** module within that container, set
the widths of **.main** and **.other** to `566px` and `331px`, respectively, and finally floated the two columns opposite each other.

![blog-result-pixels](./blog-result-pixels.png)

But the problem here is that the result is downright `inflexible`. Fixed at a width of `960px`, our page is indifferent to changes in `viewport size`, forcing a `horizontal scrollbar` upon the reader if the window drops even slightly below `1024 pixels`.

#### From pixels to percentages

Instead of pasting the `pixel values` from our comp directly into our `CSS`, we need to express those `widths` in relative, *proportional* terms. Once we’ve done so, we’ll have a `grid` that can resize itself as the `viewport` does, but without compromising `the design’s original proportions`.

Remember, there’s absolutely nothing wrong with `fixed-width layouts`! But to move toward a more `flexible grid`, let’s start with a percentage value to replace that `960px`:

```css
.page {
 margin: 36px auto;
 width: 90%;
}
```

I’ll confess that I arrived at `90%` somewhat arbitrarily, doing a bit of trial and error in the browser window to see what looked best. By setting our **.page** element to a percentage of the `browser window`, we’ve created a `container` that will expand and contract as the `viewport does`.

Since **.blog** is nested within the **.page** element, we’ve got our context—namely, `960 pixels`, the width of **.page** as it was designed in the mockup. So let’s divide our `target width` for **.blog** (900) by its `context` (960):

`900 ÷ 960 = 0.9375`

By moving the decimal over two places we’re left with 93.75%, a percentage we can drop directly into our CSS:

```css
.blog {
 margin: 0 auto 53px;
 width: 93.75%; /* 900px / 960px */
}
```

Our `left-hand content column` is floated to the left, and set at `566px`; the `additional content` is floated opposite, sized at a width of `331px`. Once again, let’s replace those pixel-based target widths with percentages. 
> But before we drop those values into our **target ÷ context = result** formula, it’s important to note that our *context has changed*.

Since they’re nested inside **.blog**, we need to express our `columns’ widths` in relation to 900px—the width of the blog. So we’ll divide our two `target values` (566px and 331px) by 900px, our new `context`:

`566 ÷ 900 = .628888889   ;   331 ÷ 900 = .367777778`

Once we move our decimal points we’re left with 62.8888889%  and 36.7777778%, the proportional widths of **.main** and **.other**:

```css
.blog .main {
 float: left;
 width: 62.8888889%; /* 566px / 900px */
}
.blog .other {
 float: right;
 width: 36.7777778%; /* 331px / 900px */
}
```

Just like that, we’re left with a `flexible`, `grid-based layout`.

## Flexible Margins and Padding

#### Can't get no ventilation

Still we need to finish very important parts: the `title` now is flush left within it's container, and our `two columns` currently abut each other, with no `margins` or `gutters`. In our comp, there’s `48 pixels` of space between our `headline` and the `left edge of its container`. 

![heading-margin](./heading-margin.png)

Now, we could use `pixels` to set a `fixed padding-left` on our `headline` in either `pixels` or `ems`, like so:

```css
.lede {
 padding: 0.8em 48px;
}
```
This is a decent solution. **But** a fixed `value` for that `padding left` would create a `gutter` that doesn’t line up with the rest of our `fluid grid`. As our `flexible columns` expand or contract, that `gutter` would simply ignore the rest of our design’s proportions, sitting stubbornly at `48px` no matter how small or wide the design became.

We can also create `percentage-based margins` and `padding` to preserve the integrity of our flexible grid. And we can reuse the **target ÷ context = result** formula to do so.

>  it’s important to note that whether you’re setting a `flexible margin` or `padding` on an element, the `context` is always the same: it’s **the width of the element’s container**.

Since we want to set some `padding` on our **.lede** headline, our `context` is the `width` of its container—that is, our 900px-wide **.blog module**. So out comes the calculator, and we’re left with:

`48 ÷ 900 = 0.0533333333`

which translates to:

```css
.lede {
 padding: 0.8em 5.33333333%; /* 48px / 900px */
}
```

And there we have it: our `48px padding` has been expressed in `relative terms`, as a `proportion` of our `headline’s width`.

We also need a bit of `white space` to our compacted `content`. To do so, it’s worth remembering that `each column` actually has a `smaller module` contained within it: the left-hand **.blog column** contains an **.article**, while the **.other** column contains our **.recent-entries listing** . We start with the `recent entries module`. Since we know the `width` of the `element` (231px) and the `width` of its `containing column` (331px), we can simply center our module horizontally:

![inner-columns-with](./inner-columns-with.png)

```css
.recent-entries {
 margin: 0 auto;
 width: 69.7885196%; /* 231px / 331px */
}
```

Now, we could take the same approach with our `article`. But instead, let’s make it a bit more interesting. Remember the `48px padding` we set on our `headline`? Well, our `article` falls along the same `column`.
 
![article-padding](./article-padding.png)

So rather than just centering our `article` within its `container`, let’s create another `proportional gutter`. Our `target value` is `48px`. And since we’re working with `relative padding`, our `context` should be the `width` of the `article` itself. 

> But once again, since there’s no explicit width set on **.article**, we can simply use `566px`, the width of its parent (**.blog**), for our `context`:

```css
.article {
 padding: 40px 8.48056537%; /* 48px / 566px */
}
```

#### Getting negative

Now we have 

![date-place-2](./date-place-2.png)

The comp tells us our `date` should be floated to the left, and that it occupies one `69px column`. Since the `date` sits within the `470px-wide article`, we have our `context`.

![date-place](./date-place.png)

Armed with that information, let’s write some quick `CSS`:

```css
.date {
 float: left;
 width: 14.68085106%; /* 69px / 470px */
}
```

**But** there’s one key `component` missing: our `date` is currently floating neatly against the left edge of
the `article`, with the `title` and `copy` floating around it.

![date-place-3](./date-place-3.png)


What we need to do is to pull that `date` out of its `container`, and move it across the `left-hand edge` of the entire `module`. **And with `negative margins`, we can do exactly that**. And we don’t have to change our approach because the `margin` is `negative`: just as before, we simply need to express that `margin` in relation to the `width` of the element’s `container`.


If we look at the `mockup`, we can see that there are `81 pixels` from the left edge of the `date` over to the left edge of the `article`.  

![date-place-4](./date-place-4.png)

We want to express our `target value` — that `81px-wide margin` — as a percentage of `470px`, the `width` of the `date’s containing element`: `81 ÷ 470 = .17234042553191`. Do the decimal shift and slap a minus sign on there, and we’ve got our proportional, negative margin: 

```css
date {
 float: left;
 margin-left: -17.2340425531%; /* 81px / 470px */
 width: 14.68085106%; /* 69px / 470px */
}
```

#### Moving forward, flexibility

> **we need to break our habit of translating pixels from Photoshop directly into our CSS, and focus our attention on the proportions behind our designs.**

It’s about becoming *context-aware*: better understanding the `ratio-based relationships` between `element` and `container`.


## Flexible Images

What if we could write a rule that prevents `images` from exceeding the `width` of their `container`? Well, here’s the good news: that’s very easy to do.

```css
img {
 max-width: 100%;
}
```

>  Now, our `img element` will render at whatever `size` it wants, as long as it’s narrower than its containing `element`. But if it happens to be wider than its `container`, then the `max-width: 100% directive` forces the `image’s width` to match the `width of its container`.

What’s more, modern `browsers` have evolved to the point where they resize the `images` proportionally: as our `flexible container` resizes itself, shrinking or enlarging our `image`, the image’s aspect ratio remains intact.

**The max-width: 100% rule** can also apply to most `fixed-width elements`, like video and other rich media. In fact,
we can beef up our selector to cover other media-ready elements, like so:

```css
img,
embed,
object,
video {
 max-width: 100%;
}
```

####  Max-width in Internet Explorer

The cold, hard truth is that `Internet Explorer 6` and below don’t support the `max-width` property. 

`CSS-driven approach`

Namely, all modern browsers get our `max-width` constraint:

```css
img,
embed,
object,
video {
 max-width: 100%;
}
```

But in a **separate** `IE6-specific stylesheet`, I’ll include the following:

```css
img,
embed,
object,
video {
 width: 100%;
}
```

IE6 and lower get `width: 100`%, rather than the `max-width: 100%` rule.

> tread carefully here, for these are drastically different rules. Whereas `max-width: 100%` instructs our `images` to *never exceed* the width of their `containers`, `width: 100%` forces our `images` to *always match* the `width` of their `containing elements`. 

Most of the time, this approach will work just fine.

For example, it’s safe to assume that our oversized `robot.jpg` image will always be larger than its containing element, so the `width: 100% rule` works beautifully. But for `smaller images` like thumbnails, or most embedded
movies, it might not be appropriate to blindly up-scale them with `CSS`. If that’s the case, then a bit more `specificity` might be warranted for `IE`:

```css
img.full,
object.full,
.main img,
.main object {
 width: 100%;
}
```

If you don’t want the `width: 100%` rule to apply to every piece of `fixed-width media` in your page, we can simply write a list of `selectors` that target certain kinds of `images` or `video` (**img.full**), or certain areas of your `document` where you know you’ll be dealing with `oversized media` (**.main img**, **.main object**). Think of this like a whitelist: if `images` or other `media` appear on this `list`, then they’ll be `flexible`; otherwise, they’ll be `fixed` in their stodgy old pixel-y ways. So if you’re still supporting legacy versions of Internet Explorer, a carefully applied `width: 100% rule` can get those `flexible images` working beautifully. 

#### FLEXIBLY TILED BACKGROUND IMAGES

Let’s say our dearly esteemed designer sends over `a revised mockup` of our `blog module`. The `design` has been modified slightly, adding a `two-toned background` to the `blog entry` to provide more contrast between the left- and righthand `columns`. What’s more, there’s actually a subtle level of noise added to the `background`, adding an extra level of texture to our `design`. So: how do we actually add this `new background image` to our `template`?

![background](./background.png)

First, we’ll begin by taking a look at our `mockup`, to find the `transition point` in our `background` graphic, the exact `pixel` at which our white column transitions into the gray. And from the look of things, that switch happens at the `568 pixel mark`.

![background-transition](./background-transition.png)

First, we’ll convert that `transition point` into a `percentage-based value` relative to our `blog module’s width`. And to do so, our **target ÷ context = result** formula comes into play yet again. We have our `target` value of `568px`, and the `width` of the design—our `context` — is `900px`. And if we plug those two values into our stalwart formula:

`568 ÷ 900 = 0.631111111111111`

Now, let’s open up your favorite `image editor`, and create a foolishly wide document — say, one that’s `3000 pixels` across. And since we’re going to tile this `image` vertically, its height is only `160px` tall.
In a moment, we’re going to turn this blank `document` into our `background graphic`. But why is it so large? Well, this `image` needs to be larger than we can reasonably assume the `browser` window will ever be. 

To create the `columns` themselves, we’ll need to apply the `transition point percentage` (**63.1111111111111%**) to our new, wider `canvas`. So if we’re working with a graphic that’s `3000px across`, we simply need to multiply that `width` by the `percentage`, like so:

`3000 x 0.631111111111111 = 1893.333333333333`

![background-columns](./background-columns.png)

