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

> 
```js
setState(prevState => {
  // Object.assign would also work
  return {...prevState, ...updatedValues};
});
```
> Another option is `useReducer`, which is more suited `for managing state objects that contain multiple sub-values`.

### **Example**: Updating state based on previous state

Let’s look at another example: updating the value of state based on the previous value.

We’ll build a, uh, “step tracker.” Very easy to use. Just like a Fitbit. Every time you take a step, simply click the button. At the end of the day, it will tell you how many steps you took. I’m working on securing my first round of funding as you read this.

```jsx
function StepTracker() {
  const [steps, setSteps] = useState(0);

  function increment() {
    setSteps(steps => steps + 1);
  }

  return (
    <div>
      Today you've taken {steps} steps!
      <br />
      <button onClick={increment}>I took another step</button>
    </div>
  );
}
```

First, we’re creating a new piece of state with useState, initializing it to 0. It returns the current value of steps (0) and a function for updating it. We have an increment function to increase the step counter.

You’ll notice we’re using the functional or “updater” form of setSteps here. We could just call setSteps(steps + 1) and it would work the same in this example, but I wanted to show you the updater form, because **it’ll be useful in case your update is happening in a closure which has closed over the old (stale) value of the state**. **Using the updater form ensures you are operating on the latest value of state.**

Another thing we’ve done here is to extract the increment function, instead of inlining the arrow function on the button’s onClick prop. We could have written button this way and it would’ve worked just the same:

```jsx
<button onClick={() => setSteps(steps => steps + 1)}>
  I took another step
</button>
```

### Example: state with multiple keys

Let’s look at an example where state is an object. We’ll make a login form with 2 fields: username and password.

I’ll show you how to store multiple values in one state object, and how to update individual values.

```jsx
function LoginForm() {
  const [form, setValues] = useState({
    username: '',
    password: ''
  });

  const printValues = e => {
    e.preventDefault();
    console.log(form.username, form.password);
  };

  const updateField = e => {
    setValues({
      ...form,
      [e.target.name]: e.target.value
    });
  };

  return (
    <form onSubmit={printValues}>
      <label>
        Username:
        <input
          value={form.username}
          name="username"
          onChange={updateField}
        />
      </label>
      <br />
      <label>
        Password:
        <input
          value={form.password}
          name="password"
          type="password"
          onChange={updateField}
        />
      </label>
      <br />
      <button>Submit</button>
    </form>
  );
}
```