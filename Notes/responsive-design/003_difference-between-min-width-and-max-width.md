# The difference between min-width and max-width

### Basic explanation of min width & max width

There are more `breakpoints` for `devices` which you can test for. Although we are using the term as `device screens`, what we actually consider is the `screen width`. 

![width-difference](./width-difference.png)

When we are using the `min-width` we strt with the `default`

- **default**, that's gonna apply any `width` from zero pixels from infinity 

If we are talking about 12 column 960 grid. The next step will be 

- **min-width 320**, it means that prior the screen being 320px wide, it's not gonna load the style information, but once it hits 320 px through infinity it's gonna load the style information. **And that style information is gonna override the default**

- **min-width 640**, at that point it will overwrite the rules of `min-width 320`

- **min-width 960**,  at that point it will overwrite the rules of `min-width 640`

When you use the `minimum width` you need to put the `smallest values` at the top of the stylesheet. 

If we are using `maximum width` it's different. 

- **max-width 320** - anything up to and including 320 px will load this particular style information. So we start from "zero" from the very first rule

- with **max-width 640** we overwrite everything, same thing width **max-width 960** 

- default - would have to be capable of overwriting everything

Here in the stylesheet we first need to include `max-width 960`

> Using the `min-width` we load only the things that are applicable to the screen of the small and smaller sizes => we won't load e.g huge images => to reduse the amount of overhead of small browsers