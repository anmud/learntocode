# Creating Stocks Component

In the `Stocks.vue` component we want kind of loop through our `individual stocks` and output them in the `Stocks.vue` component. And now let's let a `bootstrap` place them in a `grid` problematic. Therefore let's create first some "example" stocks just for the purpose we can see something while building, and we'll replace this later. So, in our `data object` we'll return an `array` of stocks. Well, how will `stocks` will be defined in our application? We'll have an `id` for each `stock`, a `name` for each `stock` and a `price` for each stoke. We'll have four individual stocks in general. 

**Stocks.vue**
```html
<template>
<div>
    
    
</div>

</template>

<script>
export default {
 data(){
     return{
         stocks: [                             //create individual stocks
             {id: 1, name: BMW, price: 110},
             {id: 2, name: Google, price: 200},
             {id: 3, name: Apple, price: 250},
             {id: 4, name: Twitter, price: 8},
         ]
     }
 }
}
</script>
```

Now with these stocks in place we want to loop through them and create as many `Stock.vue` components as needed. For that let's go to our `Stock.vue` component in the `stocks folder`. Well here let's start with layout first. We wanna have some boxes which then will be distributed by bootstrap.  We'll sertainly wrap the `stock` in its own column class `class="col-sm-6 col-md-4` so that we can fit three column boxes in the medium size screen, two of them in a small screen. Inside this `div` we'll create a `div` which uses a `panel panel-success` class, this will give green panal like look; inside we'll have a `div` with a panel heading and `h3` tag where we'll output the `name` of the stock. And let's use one more feature the bootstrap offers us - `small` and some extra data - which will fit nicely by bootstrap. 

**Stock.vue/Stocks**
```html
<template>
<div class="col-sm-6 col-md-4">
    <div class="panel panel-success">
    <div class="panel-heading">
        <h3 class="panel-title">NAME<small>(Price: PRICE)</small></h3>
    </div> 
    </div> 

</div>
</template>
```

After our `panel-heading` we want to have `panel-body` which hold the `content`. The `content` actually - is two `divs`, one is the `input form` and another is the `buy button`. The `input form` we'll have in the `pull-left div`; the `button` we'll have in the `pull-rught div`.

**Stock.vue/Stocks**
```html
<template>
<div class="col-sm-6 col-md-4">
    <div class="panel panel-success">
    <div class="panel-heading">
        <h3 class="panel-title">NAME<small>(Price: PRICE)</small></h3>
    </div> 
    <div class="panel-body">
      <div class="pull-left">
           <input type="number" class="form-control" placeholder="Quantity">
      </div> 
      <div class="pull-right">
           <button class="btn btn-success">Buy</button>
      </div>
    </div>
    </div> 

</div>
</template>
```

Now it's time to go back to our `Stocks.vue` file and first import the newly created `Stock.vue` component, register it as a local component, and use it, namely create as many `stock` as we need via looping through the `stocks` in the `Stocks.vue` file. 

**Stocks.vue**
```html
<template>
<div>
    <app-stock v-for="(stock, index) in stocks" :key="index"></app-stock>
    
</div>

</template>

<script>
import Stock from './Stock.vue';

export default {
 data(){
     return{
         stocks: [                             
             {id: 1, name: BMW, price: 110},
             {id: 2, name: Google, price: 200},
             {id: 3, name: Apple, price: 250},
             {id: 4, name: Twitter, price: 8},
         ]
     }
 },
 components:{
     appStock: Stock
 }
}
</script>
```