# Adding a Portfoliio Module to Vuex

Time to make the `buy buttons` work and for that we need a `portfolio` and some `state` for this `portfolio`. In the `modules folder` let's add a `portfolio.js` file, where we'll have the `state`. What is the `state` of our `portfolio`? We want to have some `funds` to work with and some `socks` - `stocks` here refers to the `stocks` in our `portfolio` not to all the `stocks` available. Then we need some `mutations`, this is what allows us to change our `state`, first we want to be able to buy a stock, so we'll have `buy_stock` mutation which gets the `state` and the `object` as the second `argument`, we'll pull out the `stockId`, `quantitiy` and the `stock price`.  Where do these three names in the `object` come from? How do we know that we get these three `properties`? That's basically our `order`. If we look at the `Stock.vue` file in the `stocks folder` this is how we setup our `order`. Then in the `buy_stock()` method we firts have to check if we have the stocks in our `stocks array`; so we'll create a `record` variable and access our `sate` and `stocks array` in there and then execute `find()` method, which allows us to find something in the `array`. `find()` takes a `function` as an argument where the `element` will be passed in automatically, so this automatically loop through all our elements, and then execute this `function` for each of the element; then we'll check if `element.Id == stockId`, this will terurn `true` if the `element.id` through we loop mathces the `stockId` we wanna buy. So, if our `array` is empty this will never match, but if the `array` has this `stock` already it will match at some point and therefore it return `true` of `false` which again leads to the `find()` method to return the stock in the array. And we know if `record` is set, then we already have the `stock` in the `array` and therefore we don't want to push a new item in the `array`, instead we want to take this `record` (which is the stock which was found in our array) and update the `quantity` to be the `old quantity` + the `new quantity` we are getting in the `order`. If it's not the case then we know it's a `new record` and in this case we will take our `state` and `stocks` in there and `push()` a new `object` on it, this `new object` will have an `id`, `quantity` - that's the `data` we wanna store in the `stocks array` in our `portfolio`. 

**portfolio.js**
```js
const state = {      //create state
funds: 10000,
stocks: []
};

const mutations = {        //create mutations
'BUY_STOCK'(state, {stockId, quantity, stockPrice}){
    const record = state.stocks.find( element => element.id == stockId )
    if (record){
    record.quantity += quantity;
    } else{
      state.stocks.push({
        id: stockId,
        quantity: quantity
      })
    }
}
};
``` 

The next `mutation` we need is `Sell_stocks` method. Here we'll also get a `state` and `order`, and in the `method` we'll first find the `stock` by `id` in our `array` with the `find()` method.  And hen we'll check if the `record.quantity` is greater than the `quantity` of what we want to sell, then we wanna update the `record quantity` to be the `old quantity` minus the `quantity` of the `order`. But if we try to sell more than we have, or exactly the amount we have, we want to remove it from the `array` with the `splice()` method, splice and find the position of our `record` (`indexOf record`). This will give us back a new `array` without that `item` inside of it. Of cource we need to update our `funds`, so in the `Sell_Stocks` method we'll check the `funds` and add `stock price` multiplied by the `quantity`. Actually we should also update the `funds` in the `Buy_stock` method.

**portfolio.js**
```js
const state = {     
funds: 10000,
stocks: []
};

const mutations = {        //create mutations
'BUY_STOCK'(state, {stockId, quantity, stockPrice}){
    const record = state.stocks.find( element => element.id == stockId )
    if (record){
    record.quantity += quantity;
    } else{
      state.stocks.push({
        id: stockId,
        quantity: quantity
      })
    }
    state.funds -= stockPrice * quantity; 
},
'SELL_STOCK' (state, {stockId, quantity, stockPrice}){
     const record = state.stocks.find( element => element.id == stockId )
     if(record.quantity > quantity ){
         record.quantity -= quantity;
     } else{
       state.stocks.splice(state.stocks.indexOf(record, 1));
     }
     state.funds += stockPrice * quantity; 
} 
};
``` 

Now we can add `actions`, actually just one - `sell`, cos `buy action` is located in our `stoks module`. And set the `getters` here. What `getters` we need? We want to be able to get our `current portfolio of stocks`, and `funds`. In `stockPortfolio()` we get the `state` and we can also inject some other `getters`, and inside the `method` we return `state.stocks` and now since we only have the `IDs` in our `stocks array` we need to access the `stocks` on the `stocks module`   - that's why we injected the `getters` here to find the `name` and so on of the `stocks`. We can use `map()` method for that - `return state.stocks.map()` - `map()` allows us to transform each `element` in our `array`, this will automatically input the current `element` we are looping through kind of implicitly into the `callback function`, and in there we can now setup into what we want to transform the `element` we are currently add.  Here we again want to fetch the `record`, for that we'll use our `getters` and it refers to our `store getters`, of our overal store - `const record = getters.`, and there we can use the `stocks getter`, which is the `getter` we setup in the `stocks module` in the `stocks.js` file, and execute the `find()` method. Here the `stocks.id` is the `stock` we are carrently add to the `map()` method and the `element.id` refers to the `stocks array` of the `stocks module`, so all the `stocks` not just those in our `portfolio`. Then for each `record` we want to return a new `object` - that is what the `elements` in our `array` will get transformed to. We'll return `{id: stock.id, quantity: stock.quantity, name: record.name, price: record.price}`, we use `record.name` and `record.price` cos in the `local stocks` we only have `id` and `quantity`, but then we are reaching out our `overall stocks array` to also get `name` and `price`. Well, here we basically create a new `array` where we `maped()` all these values, we expanded our `object` in this `array` to not only have `id` and `quantity`, but now also `name` and `price`.
Let's work now on our `fonds getter`, it only needs a `state` and here we simply wanna return `state.funds`, of course referring to the `funds` in the `state` of `portfolio.js` file. 

**portfolio.js**
```js
const state = {     
funds: 10000,
stocks: []
};

const mutations = {        //create mutations
'BUY_STOCK'(state, {stockId, quantity, stockPrice}){
    const record = state.stocks.find( element => element.id == stockId )
    if (record){
    record.quantity += quantity;
    } else{
      state.stocks.push({
        id: stockId,
        quantity: quantity
      })
    }
    state.funds -= stockPrice * quantity; 
},
'SELL_STOCK' (state, {stockId, quantity, stockPrice}){
     const record = state.stocks.find( element => element.id == stockId )
     if(record.quantity > quantity ){
         record.quantity -= quantity;
     } else{
       state.stocks.splice(state.stocks.indexOf(record, 1));
     }
     state.funds += stockPrice * quantity; 
}
};

const actions = {            //set actions
    sellStock ({commit}, order ){
        commit('SELL_STOCK', order);
    }
};

const getters = {
 stockPortfolio (state, getters){
  return state.stocks.map(stock => {
      const record = getters.stocks.find(element => element.id == stock.id );
      return {
        id: stock.id,
        quantity: stock.quantity,
        name: record.name,
        price: record.price
      }
  } )
 },
 funds(state){
     return state.funds;
 }
};
``` 

With that in place we need to just export it. 

**portfolio.js**
```js
const state = {     
funds: 10000,
stocks: []
};

const mutations = {        //create mutations
'BUY_STOCK'(state, {stockId, quantity, stockPrice}){
    const record = state.stocks.find( element => element.id == stockId )
    if (record){
    record.quantity += quantity;
    } else{
      state.stocks.push({
        id: stockId,
        quantity: quantity
      })
    }
    state.funds -= stockPrice * quantity; 
},
'SELL_STOCK' (state, {stockId, quantity, stockPrice}){
     const record = state.stocks.find( element => element.id == stockId )
     if(record.quantity > quantity ){
         record.quantity -= quantity;
     } else{
       state.stocks.splice(state.stocks.indexOf(record, 1));
     }
     state.funds += stockPrice * quantity; 
}
};

const actions = {            //set actions
    sellStock ({commit}, order ){
        commit('SELL_STOCK', order);
    }
};

const getters = {
 stockPortfolio (state, getters){
  return state.stocks.map(stock => {
      const record = getters.stocks.find(element => element.id == stock.id );
      return {
        id: stock.id,
        quantity: stock.quantity,
        name: record.name,
        price: record.price
      }
  } )
 },
 funds(state){
     return state.funds;
 }
};

export default{        //export all properties
  state,
  mutations,
  actions,
  getters
}
``` 
