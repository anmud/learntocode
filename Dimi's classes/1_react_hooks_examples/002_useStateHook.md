# useState Hook

```js
const [state, setState] = useState(initialState);
```

Returns a `stateful value`, and a `function` to update it.

During the `initial render`, the `returned state` (state) is the same as the `value passed as the first argument (initialState)`.

The `setState function` is used to `update` the `state`. It accepts a `new state value` and enqueues a re-render of the component.

```js
setState(newState);
```

During subsequent re-renders, the first value returned by `useState` will always be the `most recent state` after applying updates.

**Note**

> React guarantees that `setState` function identity is stable and won’t change on re-renders. This is why it’s safe to omit from the `useEffect` or `useCallback` dependency list.

## Functional updates

If the `new state` is computed using the `previous state`, you can pass a `function` to `setState`. The `function` will receive the previous `value`, and return an `updated value`. Here’s an example of a `counter` component that uses both forms of `setState`:

```js
function Counter({initialCount}) {
  const [count, setCount] = useState(initialCount);
  return (
    <>
      Count: {count}
      <button onClick={() => setCount(initialCount)}>Reset</button>
      <button onClick={() => setCount(prevCount => prevCount + 1)}>+</button>
      <button onClick={() => setCount(prevCount => prevCount - 1)}>-</button>
    </>
  );
}
```

**Note**

> Unlike the setState method found in class components, useState does not automatically merge update objects. You can replicate this behavior by combining the function updater form with object spread syntax:

> ```js
setState(prevState => {
  // Object.assign would also work
  return {...prevState, ...updatedValues};
});
```
> Another option is `useReducer`, which is more suited `for managing state objects that contain multiple sub-values`.