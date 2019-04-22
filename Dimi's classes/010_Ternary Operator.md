# Ternary Operator

A `ternary expression` is a `conditional expression` that evaluates to a `value`. It consists of a `conditional`, a truthy clause (the value to produce if the conditional evaluates to a truthy value), and a `falsy clause` (the value to produce if the conditional evaluates to a falsy value).

They look like this:

```js
(conditional)
  ? truthyClause
  : falsyClause
```

When you remove `if statements` from your `code`. Your code becomes easy to reason about.

How to remove `if statements`? We can use  a `ternary operator`.

1. Variant of a `function` with `if statement`

```js
const user = {
  isAdmin: true,
  name: "Anastasia"
}

const checkAdminStatus = data => {
  const {isAdmin} = data
  if(isAdmin){
  return 'user is Admin'
  } else  return 'user is not Admin'
}

console.log(user) // "user is Admin"
```

2. `Ternary operator` always evaluates to a `value`. Variant of a `function` without `if statement`. Instead we use a `ternary operator`.

- if true (?)
- else (:)

```js
const user = {
  isAdmin: true,
  name: "Anastasia"
}

const checkAdminStatusNoIf = ({isAdmin, name}) => {
  return (isAdmin && name === "Anastasia")
  			? "user is Admin"
  			: "user is not Admin"
}

console.log(user) // "user is Admin"
```
3. We also can use `nested ternary operator`

```js
const user2 = {
  isAdmin: false,
  name: "Anastasia"
}
// (?) then 
// (:) else
const check = ({isAdmin, name}) => {
  return isAdmin
  			? "user is Admin"
  			: name === "Dimitri"
  				? "admin is Dimitri"
  				: "admin is not Anastasia"
}


console.log(
  check(user2) // "admin is not Anastasia"
)
```

#### Chained ternaries have several advantages over if statements:

- It’s always easy to write them so that they read in a straight line, top to bottom. If you can follow a straight line, you can read a chained ternary.
- Ternaries reduce syntax clutter. Less code = less surface area for bugs = fewer bugs.
- Ternaries don’t need temporary variables, reducing load on working memory.
- Ternaries have a better signal-to-noise ratio.
- If statements encourage side effects and mutation. Ternaries encourage pure code.
- Pure code decouples our expressions and functions from each other, so ternaries train us to be better developers.
