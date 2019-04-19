# Ternary Operator

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

2. `Ternary operator` always evaluates to a `value`. Variant of a `function` without `if statement`. Instead we use `ternary operator`

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
