# Project Setup and Planning

We start from the initial state, it it `webpack-simple` installed with `Vue-cli`, and we have the following files:

**App.vue**

```html
<template>
    <div class="container">

    </div>
</template>

<script>

    export default {

    }
</script>

<style>

</style>
```

**main.js**
```js
import Vue from 'vue'
import App from './App.vue'

new Vue({
  el: '#app',
  render: h => h(App)
})
```

**index.html**
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <title>Stock Trader</title>
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css" integrity="sha384-BVYiiSIFeK1dGmJRAkycuHAHRg32OmUcww7on3RYdg4Va+PmSTsz/K68vbdEjh4u" crossorigin="anonymous">
  </head>
  <body>
    <div id="app">
    </div>
    <script src="/dist/build.js"></script>
  </body>
</html>
```
Since we are going to use `Vuex` we need to install the `stage 2 preset` too, which gives us which gives us access to the `spread operator` - so, to install `npm install --save-dev babel-preset-stage-2`. Once this downloaded we can go to the `babelrc` file and add it to our presets. 

**babel.rc**
```js
{
  "presets": [
    ["es2015", { "modules": false }],
    ["stage-2"]          //add preset here 
  ]
}
```

Let's plan our app now: we'll have a header - so it could be one separate `component`, and then we'll have three `routes`: at the `home page`, the `stocks page` where we could buy stocks, and the `portfolio page` where we can look at our stocks and sell them. Well, it sounds like we at least need four `components`. For the `individual stocks` on the `stocks page` and the `portfolio page` we probably will also need some extra `components` 