# Pure functions

A `pure function` is a function that creates and returns `value`, based only on the `input parameters` and it causes no `side effects`. 

## Pure functions rules: 

1. Must have `input parameters`

2. No `stateful values`
E.G. the `function` must not depend on any variables outside of themselves  

3. Must return a `value` that is determined by its `input parameters`

4. No side effects 

`Side effect` - when the code causes some change outside of itself. If you run a `function` and after the `function` has completed the code in the `function` has directly cause some sort of permanent change.  E.g: 

-- saving something to a database
-- writing to a file 
-- making changes to what's seen on the webapp

## Why use pure functions?:

1. they are reusable
2. they are composable, which means you can combine `functions` to effectively create new functions
3. easy to test
4. always produce the same result for a given input, so it's easy to cache expensive function calls 
 