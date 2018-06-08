# Challenge

1. Pass in some `content` to each of the `template`.
2. Hook up the `buttons` and some `templates` so, that only one of the templates is displayed, and other two are not, and we can switch them.

Here is our project folder structure. 

![slot-project](../slot-project.png)

### Solution

**App.vue**

```html
<template>
    <div class="container">
        <div class="row">
            <div class="col-xs-12">
                <br>
                <button class="btn btn-primary" @click="selectTemplate='appBlue'">Load Blue Template</button>
                <button class="btn btn-success" @click="selectTemplate='appGreen'" >Load Green Template</button>
                <button class="btn btn-danger" @click="selectTemplate='appRed'">Load Red Template</button>
                <hr>
                <component :is='selectTemplate'>
                 <p>The Content</p>
                </component>
            </div>
        </div>
    </div>
</template>

<script>
    import Blue from './components/Blue.vue';
    import Green from './components/Green.vue';
    import Red from './components/Red.vue';

    export default {
        components: {
            appBlue: Blue,
            appGreen: Green,
            appRed: Red
        },
        data: function(){
            return{
                selectTemplate: 'appBlue'
            };
        }
    }
</script>

<style>
</style>
```

**Blue.vue**

```html
<template>
    <div>
        <slot></slot>
        
    </div>
</template>

<script>

</script>

<style scoped>
    div {
        border: 1px solid blue;
        background-color: lightblue;
        padding: 30px;
        margin: 20px auto;
        text-align: center
    }
</style>
```
**Green.vue**
```html
<template>
    <div>
        <slot></slot>
    </div>
</template>

<script>

</script>

<style scoped>
    div {
        border: 1px solid green;
        background-color: lightgreen;
        padding: 30px;
        margin: 20px auto;
        text-align: center
    }
</style>
```
**Red.vue**

```html
<template>
    <div>
        <slot></slot>
    </div>
</template>

<script>

</script>

<style scoped>
    div {
        border: 1px solid red;
        background-color: lightcoral;
        padding: 30px;
        margin: 20px auto;
        text-align: center
    }
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
    <title>Vue Components</title>
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css" integrity="sha384-BVYiiSIFeK1dGmJRAkycuHAHRg32OmUcww7on3RYdg4Va+PmSTsz/K68vbdEjh4u" crossorigin="anonymous">
  </head>
  <body>
    <div id="app">
    </div>
    <script src="/dist/build.js"></script>
  </body>
</html>
```

![slot-project2](../slot-project2.png)
![slot-project3](../slot-project3.png)
![slot-project4](../slot-project4.png)

**NOTES**

Sometimes, the concept of `slots` gets confused with the idea behind `props`. Keep in mind: `slots` allow you to directly distribute some content in the `child component's template`. You pass the content between the opening and closing `selector` of that `component`.

*Example:*

```html
<child-component>
    <h1>This header will be rendered in the Child Component (if it offers a slot)
</child-component>
```
`Props` on the other hand allow you to pass `data` to a `child component` where it then is available as a `property`. You can output it in the `child component's template` (via `{‌{ }}`  or `v-bind` ) but you can also use it in the `JS code` of the `child component`. That's not (easily) possible with `slots`.

*Example:*

```html
<child-component :userId="1"></child-component>
<!-- In child component-->
props: ['userId'] // => Use as a normal property
```