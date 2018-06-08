# Creating the Application Components

Let's start with working on the `QuoteGrid` component. In the template we need to create a `div` with a class of `row`, this shall hold our quotes. Inside we will have our `Quote` component and we surely use `v-for` to replicate it as needed inside of that row. We also need to get the `array of quotes` from outside. So, in the `script` tag we'll export the default `object` and this `object` shall have some `props` named 'quotes' which are passed from outside, to have access to them. With quotes available we can loop through them as soon as we have our `Quote.vue` component.  

**QuotesGrid**

```html
<template>

<div class="row">
    
</div>

</template>

<script>
    export default{
        props: ['quotes']
    }
</script>

<style></style>
```

In our single `Quote` component we wanna setup `.panel-body` style (this is a bootstrap class). The font we setup beforehand in our `index.html` file. We'll also have a `quote` class here. And when hovering on the quote we wanna change the backgroung color. 

What we else wanna have in our `Quote` component template, is a `div` with a `class` of `col-sm-6 col-md-4 col-lg-3` for different styles in different view ports. And in there we'll use a `div` with bootstrap classes `panel` and `panel-default` to give it look basically. And inside this `div` we;ll have one more `div` with `panel-body` class and also our `quote` class. In a `div` we simply wanna have a `slot` because the `quote` content should come from outside, so, that the thing passing-in the content is the thing deciding how it should look like. Here we only create a place where it will be rendered in the end. And the thing which decides - it should be the holder of that content - and this holder decides how content should look like. The holder of the content of course is our `QuoteGrid` component. 

**Quote**
```html
<template>
<div class="col-sm-6 col-md-4 col-lg-3">

    <div class="panel panel-default">

        <div class="panel-body quote">
            <slot></slot>
        </div>

    </div> 

</div>
</template>

<script>
</script>

<style>
    .panel-body{
    font-family: 'Arizonia', cursive;
    font-size: 24px;
    color: #6e6e6e;
    }
    .quote{
        cursor: pointer;
    }
    .quote:hover{
      background-color: #ffe2e2;
    }

</style>
```

Our `QuoteGrid` component already have the quotes, and now with our single `Quote` component being created we can next loop through all quotes to render the single `Quote` for each loop and pass the content to it. 