# Directives

`Directives` - tiny pieces of `HTML attributes` that Vue offers us. It basically attaches some little piece of functionality to HTML markups.  

* `v-text` - similar to using mustache templates
* `v-html` - great for strings that have `html elements` that need to be rendered!
* `v-if`/ `v-show` - is a `conditional` that will display information depending on meeting a requirement. This can be anything- `buttons`, `forms`, `divs`, `components`.
* `v-if`/`v-else` - pretty straightforward - you can conditionally render one thing or another. There's also `v-else-if`
* `v-else-if`
* `v-for` - loops through a set of `values`. can also do a static number 
* `v-on`( or `@`) - extremely useful so there's a shortcut! `v-on` is great for binding to `events` like `click` and `mouseenter`. You're able to pass in a `parameter` for the `event` like `(e)`. We can also use ternaries directly.
* `v-bind` (or `:`) - one of the most useful directives so there's a shortcut! We can use it for so many things - class and style binding, creating dynamic props, etc...
* `v-model` - creates a relationship between the `data` in the `instance/component` and a `form input`, so you can dynamically update `values`.
* `v-pre` - will print out the inner text exactly how it is, including code (good for documentation)
* `v-cloak`
* `v-once` - will not update once it's been rendered.

### Modifiers

* `v-model.trim` will strip any leading or trailing whitespace from the bound string.
* `v-model.number` changes `strings` to `number` inputs
* `v-model.lazy` won’t populate the content automatically, it will wait to bind until an `event` happens. (It listens to change `events` instead of `input`)
* `@mousemove.stop` is comparable to `e.stopPropogation()`
* `@mousemove.prevent` this is like `e.preventDefault()`
* `@submit.prevent` this will no longer reload the page on submission
* `@click.once` not to be confused with v-once, this click event will be triggered once.
* `@click.native` so that you can listen to native events in the `DOM`

[keyCodes](https://vuejs.org/v2/api/#keyCodes)
CSS-TRICKS [vue guide](https://css-tricks.com/guides/vue/)

