# Template Literals

## Introduction to Template Literals

**Template Literals** are a new ES2015 / ES6 `feature` that allows you to work with `strings` in a novel way compared to ES5 and below.

The `syntax` at a first glance is very simple, just use `backticks` instead of single or double quotes:

```js
const a_string = `something`
```

They are unique because they provide a lot of `features` that normal `strings` built with quotes do not, in particular:

- they offer a great `syntax` to define `multiline strngs`
- they provide an easy way to interpolate `variables` and `expressions` in `strings`
- they allow you to create `DSLs` with `template tags` (DSL means domain specific language, and it’s for example used in React by Styled Components, to define CSS for a component)

## Multiline strings

Once a template literal is opened with the backtick, you just press enter to create a new line, with no special characters, and it’s rendered as-is:

```js
const string = `Hey
this

string
is awesome!`
```
**Keep in mind** that `space` is meaningful, so doing this:

```js
const string = `First
                Second`
``

is going to create a string like this:

```html
First
                Second
```

An easy way to fix this problem is by having an empty `first line`, and appending the `trim() method` right after the closing `backtick`, which will eliminate any space before the first character:

```js
const string = `
First
Second`.trim()
```

## Interpolation

**Template literals** provide an easy way to interpolate `variables` and `expressions` into `strings`.

You do so by using the `${...}` syntax:

```js
const myVariable = 'test'
const string = `something ${myVariable}` //something test
```

inside the `${}` you can add anything, even `expressions`:

```js
const string = `something ${1 + 2 + 3}`
const string2 = `something ${doSomething() ? 'x' : 'y'}`
```

## Template tags

**Tagged templates** is one `feature` that might sound less useful at first for you, but it’s actually used by lots of popular libraries around, like `Styled Components` or `Apollo`, the `GraphQL client/server lib`, so it’s essential to understand how it works.

In `Styled Components` template tags are used to define CSS strings:

```js
const Button = styled.button`
  font-size: 1.5em;
  background-color: black;
  color: white;
`
```

In `Apollo` template tags are used to define a `GraphQL query schema`:

```js
const query = gql`
  query {
    ...
  }
`
```

The `styled.button` and `gql` `template tags` highlighted in those examples are just `functions`:

```js
function gql(literals, ...expressions) {}
```

This `function` returns a `string`, which can be the result of any kind of computation.

**literals** is an `array` containing the `template literal content` tokenized by the `expressions interpolations`.

**expressions** contains all the `interpolations`.

If we take an example above:

```js
const string = `something ${1 + 2 + 3}`
```

**literals** is an `array` with two items. The first is `something`, the string until the first interpolation, and the second is an `empty string`, the space between the end of the first interpolation (we only have one) and the end of the string.

**expressions** in this case is an `array` with a single item, `6`.

A more complex example is:

```js
const string = `something
another ${'x'}
new line ${1 + 2 + 3}
test`
in this case literals is an array where the first item is:

;`something
another `
the second is:

;`
new line `
and the third is:

;`
test`
```
**expressions** in this case is an `array` with two items, `x` and `6`.

### The `function` that is passed those `values` can do anything with `them`, and this is the power of this kind feature.

The most simple example is replicating what the `string interpolation` does, by joining `literals` and `expressions`:

```js
const interpolated = interpolate`I paid ${10}€`
```

and this is how `interpolate` works:

```js
function interpolate(literals, ...expressions) {
  let string = ``
  for (const [i, val] of expressions.entries()) {
    string += literals[i] + val
  }
  string += literals[literals.length - 1]
  return string
}
```


(source)[https://flaviocopes.com/javascript-template-literals/]