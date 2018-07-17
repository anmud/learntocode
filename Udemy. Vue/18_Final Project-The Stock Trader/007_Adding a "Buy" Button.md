# Adding a "Buy" Button

Now we need to output `data` in our `stocks`. We surely need to add the `stock` we add in the loop to the `Stock.vue` component. We can do this using `props`. First we go to the `Stocks.vue` file and add `stock prop` and bind it to the `stock variable`, we should create in the `Stock.vue` file. 

**Stocks.vue**
```html
<template>
<div>
    <app-stock v-for="(stock, index) in stocks" :key="index" :stock="stock"></app-stock> <!--add props-->
    
</div>

</template>

<script>
import Stock from './Stock.vue';

export default {
 data(){
     return{
         stocks: [                             
             {id: 1, name: 'BMW', price: 110},
             {id: 2, name: 'Google', price: 200},
             {id: 3, name: 'Apple', price: 250},
             {id: 4, name: 'Twitter', price: 8},
         ]
     }
 },
 components:{
     appStock: Stock
 }
}
</script>
```
Then we'll create `props` in our `Stock.vue` file. 

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

<script>
export default{
    props: ["stock"]       //add props
}
</script>
```

With `props` available we can now replace our placeholders to output the actual `stock name` and `stock price` 

**Stock.vue/Stocks**
```html
<template>
<div class="col-sm-6 col-md-4">
    <div class="panel panel-success">
    <div class="panel-heading">
        <h3 class="panel-title">{{ stock.name }}<small>(Price: {{stock.price})</small></h3> <!--output here-->
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

<script>
export default{
    props: ["stock"]       //add props
}
</script>
```

And now it's time to work for our `input`. For the `input`, we want to bind it with the `data object` which holds the `quantity` property initially set to `0` and then bind it with `v-model` to the `input` in the `template`. **Note** By default, the `v-model directive` binds the `value` as a `String`. If we want to bind `quantity` as a `number`, we can add the `.number` modifier like so: `<input v-model.number="quantity" type="number" ... >`

**Stock.vue/Stocks**
```html
<template>
<div class="col-sm-6 col-md-4">
    <div class="panel panel-success">
    <div class="panel-heading">
        <h3 class="panel-title">{{ stock.name }}<small>(Price: {{stock.price})</small></h3> <!--output here-->
    </div> 
    <div class="panel-body">
      <div class="pull-left">
           <input type="number" class="form-control" placeholder="Quantity" v-model.number="quantity"> <!--bind here-->
      </div> 
      <div class="pull-right">
           <button class="btn btn-success">Buy</button>
      </div>
    </div>
    </div> 

</div>
</template>

<script>
export default{
    props: ["stock"], //add props
    data(){
        return{
            quantity:0
        }
    }
}
</script>
```

The next step is to setup the `button`. In order to setup a `button` let's add a `click listner` and will listen to let's say `buyStock` method. And in this `method` we'll create a new order. The `order` is basically a js `object` where we have our `stock.Id` property and for that we can access the `stock` we get passed via the `props`. And then for now we'll simply console.log `order` and set the `quantity` back to `0`, to reset it after the `order`. 

**Stock.vue/Stocks**
```html
<template>
<div class="col-sm-6 col-md-4">
    <div class="panel panel-success">
    <div class="panel-heading">
        <h3 class="panel-title">{{ stock.name }}<small>(Price: {{stock.price})</small></h3> 
    </div> 
    <div class="panel-body">
      <div class="pull-left">
           <input type="number" class="form-control" placeholder="Quantity" v-model="quantity"> 
      </div> 
      <div class="pull-right">
           <button class="btn btn-success" @click="buyStock">Buy</button> <!--add a click listner-->
      </div>
    </div>
    </div> 

</div>
</template>

<script>
export default{
    props: ["stock"], //add props
    data(){
        return{
            quantity:0
        }
    },
    methods:{            //create method 
        buyStock(){
          const order ={
              stockId: this.stock.id,
              stockPrice: this.stock.price, 
              quantity: this.quantity 
        };
        console.log(order);
        this.quantity = 0;
        }
    }
}
</script>
```
Also we want be sure we can't buy a negative amount of stocks. For that we'll add a new attribute binding, where we disable it under certain conditions: if `quantity` is smaller or equeal to `0`, if a `number` is an `integer`. 

**Stock.vue/Stocks**
```html
<template>
<div class="col-sm-6 col-md-4">
    <div class="panel panel-success">
    <div class="panel-heading">
        <h3 class="panel-title">{{ stock.name }}<small>(Price: {{stock.price})</small></h3> 
    </div> 
    <div class="panel-body">
      <div class="pull-left">
           <input type="number" class="form-control" placeholder="Quantity" v-model="quantity"> 
      </div> 
      <div class="pull-right">
           <button class="btn btn-success" @click="buyStock" 
           :disabled="quantity <= 0 || !Number = is.Integer(quantity)">Buy</button> <!--add a disable attribute with conditions-->
      </div>
    </div>
    </div> 

</div>
</template>

<script>
export default{
    props: ["stock"], 
    data(){
        return{
            quantity:0
        }
    },
    methods:{             
        buyStock(){
          const order ={
              stockId: this.stock.id,
              stockPrice: this.stock.price, 
              quantity: this.quantity 
        };
        console.log(order);
        this.quantity = 0;
        }
    }
}
</script>
```

Actually now we are reaching the point where it's hard to continue as long as we don't have the proper `state management` in place: cos we want to be able to check up the funds, execute the order and so on. 