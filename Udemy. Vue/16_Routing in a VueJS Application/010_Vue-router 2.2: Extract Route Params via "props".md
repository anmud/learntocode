# Vue-router 2.2: Extract Route Params via `"props"`

As of `vue-router version 2.2`, you can also bind your `route params` to `props` of the `target components`. This eliminates the need of `watch`-ing `$route` .

There are three ways of using this feature, check this official example [to learn more]: (https://github.com/vuejs/vue-router/tree/dev/examples/route-props)

You can basically either pass a `static value`, bind a `dynamic value` to `props` or use a `function` to also convert your `dynamic value`.
