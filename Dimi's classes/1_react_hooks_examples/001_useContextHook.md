# How Does the useContext Hook Work?

The **useContext Hook** provides all the same `functionality` you’d expect from the `Context API`, just packaged up into a simple to use `Hook` that you can use inside `functional components`.

And below is the  `Context object` inside of a `functional component`, using the new `useContext` Hook:

```js
import AppContext from './appContext.js';

const Example = () => {
  const context = useContext(AppContext);
  return (
    ...
  );
}
```

A `Context` provides both a `consumer` and a `provider`. When using the `useContext Hook` in React, you have to remember to pass in the whole `context object`, not just the `consumer` or `provider`.

You create a `Context object` in `React` by using `React.CreateContext`, and then passing in an initial `value`, like so:

```js
const AppContext = React.createContext({ foo: 'bar' });
```

This `AppContext object` is what should be passed as an `argument` into the `useContext Hook`. Like this:

```js
const context = useContext(AppContext);
```

