# Challenge Listening to Events

**Tasks**
1. Show an alert when the `Button` gets clicked
2. Listen to the `keydown` event and store the `value` in a `data property` (hint: `event.target.value` gives you the `value`) 
3. Adjust the example from `2)` to only fire if the `key down` is the `ENTER key` 

### Solution 1

**HTML**

```html
<div id="exercise">
   <!-- 1) Show an alert when the Button gets clicked -->
    <div>
        <button v-on:click="alertMe">Show Alert</button>
    </div>
     <!-- 2) Listen to the "keydown" event and store the value in a data property (hint: event.target.value gives you the value) -->
    <div>
        <input type="text" v-on:keydown="storeValue($event)">
        <p>{{ value }}</p>
    </div>
    <!-- 3) Adjust the example from 2) to only fire if the "key down" is the ENTER key -->
    <div>
        <input type="text" v-on:keydown.enter="storeValue($event)">
        <p>{{ value }}</p>
    </div>
</div>
```

**JS**

```js
new Vue({
        el: '#exercise',
        data: {
            value: ''
        },
        methods: {
        alertMe: function(){
        alert('Alert!');
        },
        storeValue: function(event){
        this.value = event.target.value;
        }
        }
    });
```

### Solution 2

**HTML**

```html
<script src="https://npmcdn.com/vue/dist/vue.js"></script>

<div id="exercise">
    <!-- 1) Show an alert when the Button gets clicked -->
    <div>
        <button v-on:click="alertMe">Show Alert</button>
    </div>
    <!-- 2) Listen to the "keydown" event and store the value in a data property (hint: event.target.value gives you the value) -->
    <div>
        <input type="text" v-on:keydown="value = $event.target.value">
        <p>{{ value }}</p>
    </div>
    <!-- 3) Adjust the example from 2) to only fire if the "key down" is the ENTER key -->
    <div>
        <input type="text" v-on:keydown.enter="value = $event.target.value">
        <p>{{ value }}</p>
    </div>
</div>
```

**JS**

```js
new Vue({
        el: '#exercise',
        data: {
            value: ''
        },
        methods: {
        	alertMe: function() {
          	alert('Alert!');
          }
        }
    });
```
