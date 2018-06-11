# Allowing for Quote Deletion

How can we track if a Quote gets clicked? Well, we know a couple of methods to react to that. 
Now we go to our `QuotesGrid` component where we have our `Quote` component as a selector. If we add `@click` to the component that will not work. But if we add also a `native` modifier - it tells to VueJS: "react to the click on that component if it happens on the native element of this component". So, it will basivally register the `click` here on the `div` which in the end sits in the `html code`, but since we add a `native` modifyer here it knows: "yes, even though it happens on the html code off that component - it treated like we clicked on the `app-quote`, which we can't cos that is not appended to the DOM, only the code in the template is appended to the DOM." Well, and there we could execute the `deleteQuote` method. And add our `method` to the `object`. Now how we determine which quote to delete? We need the `index of that quote` to delete the right one from the `array`. To get the `index` we go to our `v-for` loop. And we know that we can extract more that just one element, well the second `argument` will be the `current index` - `v-for="(quote,index) in quotes"`.  So, now we can pass `index` to our `deleteQuote` method - `@click.native="deleteQuote(index)`, and we get this `index` in the object too. Anf then we can use this - to `$emit` our own event, and when we emit this `event`, let's name it `quoteDeleted`, we pass the `index` as an argument - `methods:{ deleteQuote(index){ this.$emit('quoteDeleted', index)}}`.  

**QuotesGrid**

```html
<template>
<div class="row">

<app-quote v-for="(quote,index) in quotes" :key="index" @click.native="deleteQuote(index)">{{ quote }}</app-quote>

</div>
</template>

<script>
 import Quote from './Quote.vue';
 export default{
        props: ['quotes'],
        components:{
            appQuote: Quote
        },
        methods:{
            deleteQuote(index){
            this.$emit('quoteDeleted', index)
            }
        }
    }
</script>

<style></style>
```
Now we can go to the `App,vue` file where we used this grid, and in there we simply need to listen to this. Here we could listen to our onw event, the `quoteDeleted` event, and execute one nore `deleteQuote` method here  - `<app-quotes-grid :quotes="quotes" @quoteDeleted="deleteQuote"`. Now let's create the `method` in the `App.vue` object, where we get the `index` as an `argument` and inside the method we wanna access our `quotes array`, use the `splice()` method , start splicing at the position of the `index` and then splice one element - to modify the existing `array` and simply remove one element from it.   

**App.vue**

```html
<template>
    <div class="container">
    <app-new-quote @quoteAdded="newQuote"></app-new-quote>  
    <app-quotes-grid :quotes="quotes" @quoteDeleted="deleteQuote"></app-quotes-grid>
    <div class="row">
    <div class="col-sm-12 text-center">
    <div class="alert alert-info">Info: Click on a Quote to delete it!</div>
    </div>
    </div>

    </div>
</template>

<script>
import QuotesGrid from './components/QuotesGrid.vue';
import NewQuote from './components/NewQuote.vue';

    export default {
         data: function(){
            return {
            maxQuotes: 10,     
            quotes: ['Just a quote to see smth']   
            }
        },
        components:{
            appQuotesGrid: QuotesGrid,
            appNewQuote: NewQuote
        },
        methods:{
            newQuote(quote){
            this.quotes.push(quote);
            },
            deleteQuote(index){
            this.quotes.splice(index, 1)
            }
        }
    }
</script>

<style>
</style>
```