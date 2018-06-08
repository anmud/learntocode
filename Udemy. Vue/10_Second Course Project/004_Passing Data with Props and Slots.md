# Passing Data with Props and Slots

So, in our `QuoteGrid` we can us our single `Quote` component. We surely need first to import it, and to register it on the `components` property in the `object`, and then use it in the template as a tag. Of course we wanna use `v-for` on this component. And pass the content with simple string interpolation. 

**QuotesGrid**

```html
<template>

<div class="row">
    <app-quote v-for="quote in quotes">{{quote}}</app-quote>
</div>

</template>

<script>
    import Quote from './Quote.vue';

    export default{
        props: ['quotes'],
        components:{
            'app-quote': Quote
        }
    }
</script>

<style></style>
```
To display the content now we need to import the `QuoteGrid` to our `App.vue` and register it and surely use it in the template. Now we need to pass quotes to the component in the template, so we use `v-bind` the   add the property `quotes` (as an `attribute` for the `<app-quotes-grid>` selector), and it's bound to the `quotes array` from the `data object`. 

**App.vue**

```html
<template>
    <div class="container">
    <app-quotes-grid :quotes='quotes'></app-quores-grid>
    </div>
</template>

<script>
    import QuotesGrid from './components/QuotesGrid.vue';

    export default {
        components:{
            'app-quotes-grid': QuotesGrid
        },
         data: function(){
            return {
            maxQuotes: 10,     
            quotes: ['Just a quote to see smth']   
            }
        }
    }
</script>

<style>
</style> 
```

Now we can see our quote displayed. 

![first-quote](../first-quote.png)
