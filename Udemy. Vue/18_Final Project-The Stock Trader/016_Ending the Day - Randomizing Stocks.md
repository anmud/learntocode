# Ending the Day - Randomizing Stocks

Time to recalculate all `stock prices`, and for that we need to hook up `end day button`. First we go to our `Header` and add some `methods` so we can actually use our `button`.  We'll name the `method` which the `button` should trigger - "endDay", and here we wanna call the `action` we have in our `store` in the `stocks module`. For that we need to `map actions`, because a bit later we'll also need `actions` for `Save & Load` activity. And then in `methods` we'll distribute it with the `spread operator` and the name of the `action` we are interested in, namely `randomizeStocks`. And this now allows us in the `endDay()` method simply call `randomizeStocks`. 

**Header.vue**
```html
<template>
    <nav class="navbar navbar-default">
        <div class="container-fluid">
            <div class="navbar-header">
                <router-link to="/" class="navbar-brand">Stock Trader</router-link>
            </div>

            <div class="collapse navbar-collapse">
                <ul class="nav navbar-nav">
                    <router-link to="/portfolio" activeClass="active" tag="li"><a>Portfolio</a></router-link>
                    <router-link to="/stocks" activeClass="active" tag="li"><a>Stocks</a></router-link>
                </ul>
                 <strong class="navbar-text navbar-right">Funds: {{ funds | currency }}</strong>
                <ul class="nav navbar-nav navbar-right">
                    <li><a href="#" >End Day</a></li>
                    <li class="dropdown">
                        <a
                                href="#"
                                class="dropdown-toggle"
                                data-toggle="dropdown"
                                role="button"
                                aria-haspopup="true"
                                aria-expanded="false">Save & Load <span class="caret"></span></a>
                        <ul class="dropdown-menu">
                            <li><a href="#" >Save Data</a></li>
                            <li><a href="#" >Load Data</a></li>
                        </ul>
                    </li>
                </ul>
            </div><!-- /.navbar-collapse -->
        </div><!-- /.container-fluid -->
    </nav>
</template>

<script>
import {mapActions} from 'vuex';       //map actions

export default{
  computed:{
      funds(){
          return this.$store.getters.funds; 
      }
  },
  methods:{     //create methods
      ...mapActions([
          'randomizeStocks'
      ]),     
   endDay(){
     this.randomizeStocks();
   }
  }
}

</script>
```

Now let's implement the logic to recalculate `stock prices`. We go to the `stocks.js` module, and adjust `RND_STOCKS` mutation there. How can we recalculate stocks? First we access stocks (`state.stocks`) and we should do smth for `each stock` (`forEach()` method), in `forEach()` method we pass a `callback function` and then we can set `stock.price` to a `new price`. This `new price` is actually a random number, and we actually want to use the old price and then increase and decrease it a little bit - `stock.price * (1 + Math.random()`. That of cource gives us only the upside potential, now we'll deduct `0.5` from it - now we are multiplying the old price with smth between `0.5` and `1.5`. And finally we'll use `Math.round()` to have an integer. 

**stocks.js/module**
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
        commit('BUY_STOCK', order);
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

All we need to do is to add a `click listner` to the `end day button` which calls `endDay()` method. 