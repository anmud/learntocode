# Passing Content - The Suboptimal Solution

We can create `props` in our child `Quote.vue` component, use here a string interpolation to output quote. 
And in the parent `App.vue` component use `prop` with the content in the template, inside the `<app-quote>` component. 

**App.vue**

```html
<template>
    <div class="container">
        <div class="row">
            <div class="col-xs-12">
               <app-quote quote="A wonderful quote"></app-quote>  <!--use props--> 
            </div>
        </div>
    </div>
</template>

<script>
import Quote from './components/Quote.vue'
    export default {
        components:{
            'app-quote': Quote
        }
    }
</script>

<style>
</style>
```

**Quote.vue**

```html
<template>
<div>
    <p>{{quote}}</p> <!--use string interppolation to output quote-->
</div>
</template>

<script>
export default{
    props: ['quote']   //set props here 
}
</script>

<style scoped>
div{
    border: 1px solid #ccc;
    box-shadow: 1px 1px 2px black;
    padding: 30px;
    margin: 30px auto;
    text-align: center;
}

</style>
```

This way is ok, but maybe we wanna to pass in the `parent component` e.g `html code`. What should we do then? Instead it would be nice if we could pass the block of `html code` by simply enclosing it in our `quote`. 

**App.vue**

```html
<template>
    <div class="container">
        <div class="row">
            <div class="col-xs-12">
               <app-quote>          <!--enclose in the quote-->
               <h2>The Quote</h2>
               <p>A wonderful Quote!</p>
               </app-quote>  
            </div>
        </div>
    </div>
</template>

<script>
import Quote from './components/Quote.vue'
    export default {
        components:{
            'app-quote': Quote
        }
    }
</script>

<style>
</style>
```

Ind then it would be nice if we would have it in our `template`, outout it in `Quote.vue`. We can use the concept called - `slots`. VueJS offers us `slots` we can reserve for content being passed from outside. (003_Passing Content with Slots)

