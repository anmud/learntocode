# Fetching Data (GET Request)

When `loading stock` we also will trigger it in the `Header`, but we won't set all logic here too, because when loading `stocks` we change our `state`. First of all we add a `click listner` to `load data button` in the `Header` and surely the `loadData()` method. In the method we wanna execute an `action`, and that action doesn't exist yet, so let's create one. And this `action` really influences two modules: `portfolio.js` and `stocks.js` - we change the `state` in both. Therefore  let's create a new file in the `store` folder and name it `actions.js`. We need an `action` cos it will run asynchronously. In the file we'll export a `constant` "loadData" and this is a `function` where we have `commit()` function, we are not getting any `payload` here cos we are not passing one, instead here we wanna reach out to the `server`. We'll use `Vue` so that's why we first need to import it to the `actions.js`, and then use `Vue.http` - now without `$` cos we are accessing in directly on the `Vue object` itself, then `get()` method and reach `data.json`. Once we get it we need to execute `then()` cos we have a `promise` here, and inside the `then()` we want to extract the `data` and transform it into a `js object`, which also gives us back a `promise` so we need to call `then()` again, and in there we got our extracted `data`. And with that `data` we first need to check if we actually have any `data`, in case we have we'll get our `stocks`, `funds` and `stockPortfolio` from `data`. So, with that we extracted all the `data`. Now we'll create a new `portfolio object` where we'll store `stockPortfolio` and `funds`, and this of course is the `state` we'll setup in the `portfolio.js` file. And the last thing we need to do is to `commit` the `mutations`, the first is `SET_STOCKS` form `stocks.js`. And we need the same for `portfolio`, so in `portfolo.js` let's create `mutation`. And now we can commit `SET_PORTFOLIO` as well. 

**actions.js/store**

```js
import Vue from 'vue';

export const loadData = ({commit}) => {
 Vue.http.get('data.json')   //get data
 .then(response => response.json())   //transfrm the data 
 .then(data=>{
   if(data){
     const stocks = data.stocks;      //extract the data 
     const funds = data.funds;
     const stockPortfolio = data.stockPortfolio;

     const portfolio = {       //create portfolio object
       stockPortfolio,
       funds 
     };
    commit('SET_STOCKS', stocks)  //commit
    commit('SET_PORTFOLIO', portfolio)
   }
 });
};
```

**portfolio.js**
```js
const state = {     
    funds: 10000,
    stocks: []
    };
    
    const mutations = {        
    'BUY_STOCK'(state, {stockId, quantity, stockPrice}){
        const record = state.stocks.find( element => element.id == stockId )
        if (record){
        record.quantity += quantity;
        } else{
          state.stocks.push({
            id: stockId,
            quantity: quantity
          });
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
    },
    'SET_PORTFOLIO' (state, portfolio) {        //create mutation for portfolio
        state.funds = portfolio.funds;
        state.stocks = portfolio.stockPortfolio ? portfolio.stockPortfolio : [];
    }
    };
    
    const actions = {            
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

    export default{        
        state,
        mutations,
        actions,
        getters
      }
```