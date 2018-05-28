# Some Basics

**HTML**

```html
<script src="https://unpkg.com/vue/dist/vue.js"></script>

<div id="app">
  <h1 ref="heading">{{ title }}</h1>
  <button v-on:click="show">Show Paragraph</button>
  <p v-if="showParagraph">This is not always visible</p>
</div>
```

**JS**

```js
new Vue({
  el: '#app',
  data: {
    title: 'The VueJS Instance',
    showParagraph: false
  },
  methods: {
    show: function() {
      this.showParagraph = true;
      this.updateTitle('The VueJS Instance (Updated)');
    },
    updateTitle: function(title) {
      this.title = title;
    }
  },
  computed: {
    lowercaseTitle: function() {
      return this.title.toLowerCase();
    }
  },
  watch: {
    title: function(value) {
      alert('Title changed, new value: ' + value);
    }
  }
});
```
The `vue instance` is kind of the middle-man between our DOM, html code and our business logic. We pack all our business logic into our `vue instance`. 

* We can have more than one `vue instance`
* We access our `vue instance` from outside