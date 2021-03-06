# Challenge `v-if`, `v-for`

**HTML**

```html
<script src="https://npmcdn.com/vue/dist/vue.js"></script>

<div id="exercise">
  <!-- 1) Hook up the button to toggle the display of the two paragraphs. Use both v-if and v-show and inspect the elements to see the difference -->
  <div>
    <button @click="isShown = !isShown">Toggle</button>
    <p v-if="isShown">You either see me ...</p>
    <p v-else>...or me</p>
    <p v-show="isShown">You either see me ...</p>
    <p v-show="!isShown">...or me</p>
  </div>
  <!-- 2) Output an <ul> of array elements of your choice. Also print the index of each element. -->
  <ul>
    <li v-for="(name, index) in array">{{ name }} ({{index}})</li>
  </ul>
  <!-- 3) Print all key-value pairs of the following object: {title: 'Lord of the Rings', author: 'J.R.R. Tolkiens', books: '3'}. Also print the index of each item. -->
  <ul>
    <li v-for="(value, key, index) in myObject">{{ key }} : {{ value }} ({{ index }})
    </li>
  </ul>
  <!-- 4) Print the following object (only the values) and also create a nested loop for the array: {name: 'TESTOBJECT', data: [1.67, 1.33, 0.98, 2.21]} (hint: use v-for and v-if to achieve this) -->
  <ul>
    <li v-for="value in testData">
      <template v-if="Array.isArray(value)">
        <div v-for="element in value">{{ element }}</div>
      </template>
      <template v-else>
        {{ value }}
      </template>
    </li>
  </ul>
</div>
```

**JS**

```js
new Vue({
  el: '#exercise',
  data: {
    isShown: true,
    array: ['Max', 'Anna', 'Chris', 'Manu'],
    myObject: {
      title: 'Lord of the Rings',
      author: 'J.R.R. Tolkiens',
      books: '3'
    },
    testData: {
      name: 'TESTOBJECT', 
      id: 10,
      data: [1.67, 1.33, 0.98, 2.21]
    }
  }
});
```