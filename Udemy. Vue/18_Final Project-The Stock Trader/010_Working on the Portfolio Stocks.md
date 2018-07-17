# Working on the Portfolio Stocks

So, we setup our `portfolio` now we need to add it to our `store.js` by importing it first of all, add it to the `modules object` 

**store.js**
```js
import Vue from 'vue';
import Vuex from 'vuex';

import stocks from './modules/stocks';
import portfolio from './modules/portfolio'; //import here 




Vue.use(Vuex);

export default new Vuex.Store({

    modules: {
        stocks,
        portfolio           //add to the object
    }
});
```

Now we can use all the `actions`, `mutations` and `getters` to update our `Portfolio.vue` component and to make our `buy button` work. Let's work on the `buy button`. In the `Stock.vue` file of the `stocks folder` we have our `buyStock()` method and in this method we now finally want to use the `order` we created to dispatch it - ` this.$store.dispatch()`. (Of course we could also `map()` our `actions` and then call this `action` here, but for this example we'll choose `dispatch()`). And now the `name of the action` is `BuyStock` (from stocks.js module), and the `mutation` we need is in the `portfolio.js` module, yes they can be in the same module - this is just the example of the point that we can surely `commit()` mutations across `modules`. So, we `dispatch()` `buyStock` and we need also to pass the `order` as a second `argument` as our `payload`. 

**Stock.vue/stocks folder**
```html
<template>
<div class="col-sm-6 col-md-4">
    <div class="panel panel-success">
    <div class="panel-heading">
        <h3 class="panel-title">{{stock.name}}<small>(Price: {{stock.price}})</small></h3>
    </div> 
    <div class="panel-body">
        <div class="pull-left">
           <input type="number" class="form-control" placeholder="Quantity" v-model.number="quantity">
      </div> 
      <div class="pull-right">
           <button class="btn btn-success" @click="buyStock" :disabled="quantity <= 0 || !Number.isInteger(quantity)">Buy</button>
      </div>
    </div>
    </div> 

</div>
</template>

<script>
export default{
     props: ['stock'],
    data() {
        return {
            quantity: 0
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
        this.$store.dispatch('buyStock', order);        //dispatch here 
        this.quantity = 0;
        }
    }
}
</script>
```

In the `stocks.js` module `buyStock()` method doesn't do much right now, it doesn't `commit()` anything, so here we need to commit `BUY_STOCK`, and here we see this global `namespace` even though it's a different module, `BUY_STOCK` will refer to the `mutation` in the `portfolio.js` module. And surely we need to add an `order` as an `argument` to this `mutation`, so that this mutation is able to pull the `data` it needs to pull. 

**stocks.js/modules**
```js
import stocks from '../../data/stocks';

const state = {
    stocks: []
};

const mutations = {
    'SET_STOCKS' (state, stocks) {
        state.stocks = stocks;
    },
    'RND_STOCKS' (state) {
        state.stocks.forEach(stock => {
            stock.price = Math.round(stock.price * (1 + Math.random() - 0.5));
        });
    }
};

const actions = {
    buyStock: ({commit}, order) => {
        commit('BUY_STOCK', order);      // commit mutation from the portfolio.js
    },
    initStocks: ({commit}) => {
        commit('SET_STOCKS', stocks);
    },
    randomizeStocks: ({commit}) => {
        commit('RND_STOCKS');
    }
};

const getters = {
    stocks: state => {
        return state.stocks;
    }
};

export default {
    state,
    mutations,
    actions,
    getters
};
```

With that in plac we can go to the `Portfolio.vue` and make it is actually printed to the screen, if that works. For that in our `Portfolio.vue` file we need some `stock components`, like we have in `stocks module`. For that let's copy the code from the `Stock.vue` file in the `stocks component` folder and put it in the `Stock.vue` in `portfolio component`. First of all we need to get rid of the `byStock()` method and then work on the `template`. Here in the `<small>` section we;ll not only have a `price` but also `quantity`. Then we'll name the `button` "sell" instead of "buy", and the `click listner` at the `button` should now listen to `sellStock` method. And noe we surely need to add our `sellStock` method. And `sellStock` method will create an `order` as well, where we'll have `stockId`, `stockPrice` and the `quantity`. We have the access to the `price` here because in our `portfolio` module in the `store` when getting the `stockPortfolio` in the `getters` we are `mapping` each `element` in the `array` and we do add this `price` field. 

**Stock.vue/portfolio component**
```html
<template>
<div class="col-sm-6 col-md-4">
    <div class="panel panel-success">
    <div class="panel-heading">
        <h3 class="panel-title">{{stock.name}}<small>(Price: {{stock.price | Quantity: {{stock.quantity}} }})</small></h3> <!--output quantity-->
    </div> 
    <div class="panel-body">
        <div class="pull-left">
           <input type="number" class="form-control" placeholder="Quantity" v-model.number="quantity">
      </div> 
      <div class="pull-right">
           <button class="btn btn-success" @click="sellStock" :disabled="quantity <= 0 || !Number.isInteger(quantity)">Sell</button>  <!--rename the button, change click listner-->
      </div>
    </div>
    </div> 

</div>
</template>

<script>
export default{
     props: ['stock'],
    data() {
        return {
            quantity: 0
        }
    },
    methods:{
        sellStock(){            //create sell stock method 
        const order = {
            stockId: this.stock.id,
            stockPrice: this.stock.price,
            quantity: this.quantity
        }
        }
    }
}
</script>
```
The only thing we haven't do yet, we are not using the `stockPortfolio getter`. In the `Stock.vue` file of the `portfolio component` when we created the `order` we surely want to `dispatch` it. Now let's see the different way to do this, by importing `map actions` from `vuex`. In the `methods` object we'll use three dots to call `mapActions` and distribute all the `properties` this is going to create for us. And there we'll pass an `array` with `sellStock`.  This now gives us access to `this.sellStock()` for the `sellStock` method. 

**Stock.vue/portfolio component**
```html
<template>
<div class="col-sm-6 col-md-4">
    <div class="panel panel-success">
    <div class="panel-heading">
        <h3 class="panel-title">{{stock.name}}<small>(Price: {{stock.price | Quantity: {{stock.quantity}})</small></h3> 
    </div> 
    <div class="panel-body">
        <div class="pull-left">
           <input type="number" class="form-control" placeholder="Quantity" v-model.number="quantity">
      </div> 
      <div class="pull-right">
           <button class="btn btn-success" @click="sellStock" :disabled="quantity <= 0 || !Number.isInteger(quantity)">Sell</button>  
      </div>
    </div>
    </div> 

</div>
</template>

<script>
import {mapActions} from 'vuex'

export default{
     props: ["stock"],
    data() {
        return {
            quantity: 0
        }
    },
    methods:{
        ...mapActions([
          'sellStock'
        ]),
        sellStock(){            
        const order = {
            stockId: this.stock.id,
            stockPrice: this.stock.price,
            quantity: this.quantity
        };
        this.sellStock()
        }
    }
}
</script>
```