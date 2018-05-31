# How to name Components Tags (Selectors)

When we name selectors, should we use a dash (`-`) or could we use case sensitive name - like `appHeader`? Yes we can use case sensitive selectors, cos since we are using this `single file component` we don't have the DOM restriction that the DOM is case insensitive. 

If you were to use another `template` like with the `template property`, where you pass a string, or by reffering the `template` with `el`   - you would have these restrictions, cos there we use the native DOM as our `template`