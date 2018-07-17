# Time to Fix some Errors

So for now `selling the stock` doesn't work, we want to fix that and also we wanna have a small style change, and change the color of our box. So, we go to our `Stock.vue` component in the `portfolio folder` and here the box color is easily changed by changing the `panel-success` to `panel-info`. And now we have a question why `stock selling` doesn't work: we have our `sellStock()` method, we created an `order`, but we don't pass the `order` as an argument when we call our `sellStock()` method.
Also after `selling` method we want the reset our `quantity` to `0`. One thing more to fix here is that we have the same name for two `methods`: `mapActions - sellStock`, and `sellStock()` method itself. Let's change the name of `mapActions`, let's name it `placeSellOrder` and bind it to `sellStock` actions in our store in `portfolio.js` 

**Stock.vue/portfolio**

```html
<template>
<div class="col-sm-6 col-md-4">
    <div class="panel panel-info"> <!--change to panel-info-->
    <div class="panel-heading">
        <h3 class="panel-title">{{stock.name}}<small>(Price: {{stock.price}} | Quantity: {{stock.quantity}})</small></h3>
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
         ...mapActions({
             placeSellOrder: 'sellStock'    //change the name here 
         }),
     sellStock(){
        const order = {
            stockId: this.stock.id,
            stockPrice: this.stock.price,
            quantity: this.quantity
        };
        this.placeSellOrder(order)     //use the renamed method
        this.quantity = 0;            //reset the quantity 
        }
    }
}
</script>
```

To see if our `funds` work we surely need to display `funds`. Let's do this next. 