# useEffect Hook examples

The `useEffect` function is like the swiss army knife of hooks. It can be used for a ton of things, from setting up subscriptions to creating and cleaning up timers to changing the value of a ref.

1. [source](https://javascriptplayground.com/refactoring-to-react-hooks/)

**useEffect**  lets us run `side effects` in our `components`. That is, things that happen as a result of a `React component` being rendered.

```jsx
import React, { useState, useEffect } from 'react'

const DemoWithHooks = props => {

  const [user, setUser] = useState(undefined)

  useEffect(() => {
    // TODO
  })

  return (
    <pre>
      <code>{JSON.stringify(user, null, 4)}</code>
    </pre>
  )
}
```

The `value` passed to `useState` is the original `value`. This is needed for the `first render`. Here I’ve explicitly passed in `undefined` so it’s clear that when this `component` runs we don’t have a `user` yet. To get a `user`, we need to move on to the **useEffect hook**.

`useEffect` takes a `function` and runs it when the `component` renders. This means it will run both when the `component` first mounts, and when the `component` is re-rendered. Don’t worry though, we are able to have control over exactly when it is executed, and we’ll see that shortly.

Let’s fill our `useEffect` call in with a `function` that `fetches` our `user` and updates the `state`. Note that we call `setUser` from within `useEffect`. This is common if you’ve got some state that you’re setting by making an `HTTP request`.


```jsx
import React, { useState, useEffect } from 'react'

const DemoWithHooks = props => {

  const [user, setUser] = useState(undefined)

  useEffect(() => {
    fetchUser(props.id).then(setUser)
  })

  return (
    <pre>
      <code>{JSON.stringify(user, null, 4)}</code>
    </pre>
  )
}
```

When used in this manner, the `function` given to `useEffect` will be called:

- when the `component` first renders
- anytime the `component` is subsequently rendered

As it happens, for our `component` this is OK, because we only have one `prop` that could cause an update - `id`. And every time that `property` changes, we do want to `fetch` the `user’s data` again.

But, what if this `component` took many `props`, or had other `bits of state`? In that case, whenever any of those `props` changed, and the `component` was rendered again, our `fetchUser` code would run. It would do this even if `props.id` hadn’t changed, and that’s just a wasted network request if we already have the `data` for that `user`.

We would tackle this with `useEffect` by passing a `second argument` which is an `array` of `data` that has to change for the `effect` to re-run:

```js
const DemoWithHooks = props => {
  const [user, setUser] = useState(undefined)

  useEffect(
    () => {
      fetchUser(props.id).then(setUser)
    },
    [props.id]
  )

  return (
    <pre>
      <code>{JSON.stringify(user, null, 4)}</code>
    </pre>
  )
}
```
Another way to think of this `array`: it should contain every `variable` that the `effect function` uses from the surrounding scope. So if it uses a `prop`? That goes in the `array`. If it uses a `piece of state`? That goes in the `array`. 

2. 
Keep in mind we cannot use an `async function` directly inside `useEffect`. If we ever want to call an `async function`, we need to define the `function` outside of `useEffect` and then call it within `useEffect`.

```js
const fetchUsers = async () => {
    const response = await axios.get(`https://jsonplaceholder.typicode.com/users`);

    setUsers(response.data);
  };

  useEffect( () => { fetchUsers(users) }, [ users ] );
  ```

  **Note**
There are 2 important rules here.

> 1. Don't call `hooks` inside the `loop`, `condition` or `nested function`.

Instead, always use `Hooks` at the top level of your `React function`. This rule, you ensure that `Hooks` are called in the same order each time a component renders.

> 2. Call `hooks` from `react function`, not the `regular function`.

So you can `Call Hook`s from React `functional components` or from the `custom hooks` as we discussed early. By following this rule, you ensure that all stateful logic in a component is clearly visible from its source code.

3. 

```js
import React, { useEffect, useState } from 'react';
import ReactDOM from 'react-dom';

function LifecycleDemo() {
  // It takes a function
  useEffect(() => {
    // This gets called after every render, by default
    // (the first one, and every one after that)
    console.log('render!');

    // If you want to implement componentWillUnmount,
    // return a function from here, and React will call
    // it prior to unmounting.
    return () => console.log('unmounting...');
  })

  return "I'm a lifecycle demo";
}

function App() {
  // Set up a piece of state, just so that we have
  // a way to trigger a re-render.
  const [random, setRandom] = useState(Math.random());

  // Set up another piece of state to keep track of
  // whether the LifecycleDemo is shown or hidden
  const [mounted, setMounted] = useState(true);

  // This function will change the random number,
  // and trigger a re-render (in the console,
  // you'll see a "render!" from LifecycleDemo)
  const reRender = () => setRandom(Math.random());

  // This function will unmount and re-mount the
  // LifecycleDemo, so you can see its cleanup function
  // being called.
  const toggle = () => setMounted(!mounted);

  return (
    <>
      <button onClick={reRender}>Re-render</button>
      <button onClick={toggle}>Show/Hide LifecycleDemo</button>
      {mounted && <LifecycleDemo/>}
    </>
  );
}

ReactDOM.render(<App/>, document.querySelector('#root'));
```

**Why is it “unmounting” at every render?**

Well, the cleanup `function` you can (optionally) return from `useEffect` isn’t only called when the component is unmounted. It’s called every time before that effect runs – to clean up from the last run. This is actually more powerful than the `componentWillUnmount` lifecycle because it lets you run a side effect before and after every render, if you need to.

> Rather than thinking about `useEffect` - like one `function` doing the job  instead  three separate lifecycles, it might be more helpful to think - like a **`way to run side effects after render`** – including the potential `cleanup` you’d want to do before each one, and before `unmounting`.

4. **Fetch Data With useEffect**

Let’s look at another common use case: fetching data and displaying it.

Here’s a component that fetches posts from Reddit and displays them:

```jsx
import React, { useEffect, useState } from "react";
import ReactDOM from "react-dom";

function Reddit() {
  // Initialize state to hold the posts
  const [posts, setPosts] = useState([]);

  // Use an async function so that we can await the fetch
  useEffect(async () => {
    // Call fetch as usual
    const res = await fetch(
      "https://www.reddit.com/r/reactjs.json"
    );

    // Pull out the data as usual
    const json = await res.json();

    // Save the posts into state
    // (look at the Network tab to see why the path is like this)
    setPosts(json.data.children.map(c => c.data));
  }); // <-- we didn't pass a value. what do you think will happen?

  // Render as usual
  return (
    <ul>
      {posts.map(post => (
        <li key={post.id}>{post.title}</li>
      ))}
    </ul>
  );
}

ReactDOM.render(
  <Reddit />,
  document.querySelector("#root")
);
```
You’ll notice that we aren’t passing the second argument to `useEffect` here. This is bad. Don’t do this.

Passing no 2nd argument causes the `useEffect` to run every render. Then, when it runs, it fetches the `data` and updates the `state`. Then, once the `state` is updated, the `component` re-renders, which triggers the `useEffect` again. You can see the problem.

To fix this, we need to pass an array as the 2nd argument. What should be in the array?

The only `variable` that `useEffect` depends on is `setPosts`. Therefore we should pass the array `[setPosts]` here. Because `setPosts` is a setter returned by `useState`, it won’t be recreated every render, and so the effect will only run once.

Fun fact: When you call useState, the setter function it returns is only created once! It’ll be the exact same function instance every time the component renders, which is why it’s safe for an effect to depend on one. This fun fact is also true for the dispatch function returned by useReducer.


5. **Re-fetch When Data Changes**

How to re-fetch data when something changes, like a user ID, or in this case, the name of the subreddit.

First we’ll change the Reddit component to accept the subreddit as a prop, fetch the data based on that subreddit, and only re-run the effect when the prop changes:

```jsx
// 1. Destructure the `subreddit` from props:
function Reddit({ subreddit }) {
  const [posts, setPosts] = useState([]);

  useEffect(async () => {
    // 2. Use a template string to set the URL:
    const res = await fetch(
      `https://www.reddit.com/r/${subreddit}.json`
    );

    const json = await res.json();
    setPosts(json.data.children.map(c => c.data));

    // 3. Re-run this effect when `subreddit` changes:
  }, [subreddit, setPosts]);

  return (
    <ul>
      {posts.map(post => (
        <li key={post.id}>{post.title}</li>
      ))}
    </ul>
  );
}

// 4. Pass "reactjs" as a prop:
ReactDOM.render(
  <Reddit subreddit='reactjs' />,
  document.querySelector("#root")
);
```

This is still hard-coded, but now we can customize it by wrapping the Reddit component with one that lets us change the subreddit. Add this new App component, and render it at the bottom:

```jsx
function App() {
  // 2 pieces of state: one to hold the input value,
  // another to hold the current subreddit.
  const [inputValue, setValue] = useState("reactjs");
  const [subreddit, setSubreddit] = useState(inputValue);

  // Update the subreddit when the user presses enter
  const handleSubmit = e => {
    e.preventDefault();
    setSubreddit(inputValue);
  };

  return (
    <>
      <form onSubmit={handleSubmit}>
        <input
          value={inputValue}
          onChange={e => setValue(e.target.value)}
        />
      </form>
      <Reddit subreddit={subreddit} />
    </>
  );
}

ReactDOM.render(<App />, document.querySelector("#root"));
```

The app is keeping 2 pieces of state here – the current input value, and the current subreddit. Submitting the input “commits” the subreddit, which will cause Reddit to re-fetch the data from the new selection. Wrapping the input in a form allows the user to press Enter to submit.

> We could’ve used just 1 piece of state here – to store the input, and send the same value down to Reddit – but then the Reddit component would be fetching data with every keypress.

The useState at the top might look a little odd, especially the second line:

```js
const [inputValue, setValue] = useState("reactjs");
const [subreddit, setSubreddit] = useState(inputValue);
```
We’re passing an initial value of “reactjs” to the first piece of state, and that makes sense. That value will never change.

But what about that second line? What if the initial state changes? (and it will, when you type in the box)

Remember that useState is stateful (read more about useState). It only uses the initial state once, the first time it renders. After that it’s ignored. So it’s safe to pass a transient value, like a prop that might change or some other variable.

### A Hundred And One Uses

The useEffect function is like the swiss army knife of hooks. It can be used for a ton of things, from setting up subscriptions to creating and cleaning up timers to changing the value of a ref.

One thing it’s not good for is making DOM changes that are visible to the user. The way the timing works, an effect function will only fire after the browser is done with layout and paint – too late, if you wanted to make a visual change.

For those cases, React provides the useMutationEffect and useLayoutEffect hooks, which work the same as useEffect aside from when they are fired. Have a look at the docs for useEffect and particularly the section on the timing of effects if you have a need to make visible DOM changes.

> `useEffect` is run after the render. Always think: First render, then effect.

### Cleaning up from your effect

Sometimes you need to undo what you've done... to clean up after yourself when the component is to be unmounted. To accomplish this you can return a function from the function passed to useEffect... that's a mouthful but let's see a real example, of what would be both componentDidMount and componentDidUnmount combined into a single effect.

```jsx
import React, { useEffect } from "react";

default function Listen() {
  useEffect(() => {
    const listener = () => {
      console.log("I have been resized");
    };
    window.addEventListener("resize", listener);

    return () => {
      window.removeEventListener("resize", listener);
    };
  }, []);

  return <div>resize me</div>;
}
```

### Avoid setting state on unmounted components
Because effects run after the component has finished rendering, and because they often contain asynchronous code, it's possible that by the time the asynchronous code resolves, the component is no longer even mounted! When it gets around to calling the setData function to update the state, you'll receive an error that you can't update state on an unmounted component.

The way we can solve the stated (no pun intended) issue above, is by using a local variable and taking advantage of the "cleanup" function returned from our effect function. By starting it off as true, we can toggle it to false when the effect is cleaned up, and use this variable to determine whether we still want to call the setData function or not.

```jsx
import React, { useState, useEffect } from "react";
import Axios from "axios";

default function Fetcher({ url }) {
  const [data, setData] = useState(null);

  useEffect(
    () => {
      // Start it off by assuming the component is still mounted
      let mounted = true;

      const loadData = async () => {
        const response = await Axios.get(url);
        // We have a response, but let's first check if component is still mounted
        if (mounted) {
          setData(response.data);
        }
      };
      loadData();

      return () => {
        // When cleanup is called, toggle the mounted variable to false
        mounted = false;
      };
    },
    [url]
  );

  if (!data) {
    return <div>Loading data from {url}</div>;
  }

  return <div>{JSON.stringify(data)}</div>;
}
```

### Cancelling an Axios call when component unmounts
With the example above, you may have asked yourself... why even bother waiting for a response if we know for a fact we don't even need it. It turns out Axios has a way to cancel a request. We can use the same method as above, using a local variable along with an effect cleanup function, but this time the local variable will be an Axios cancellation source/token, allowing us to call source.cancel() to stop Axios in its tracks.

Just keep in mind that this will raise an exception that we should catch. Axios provides us a way using Axios.isCancel(error) to determine if what we caught was because of our own cancellation or some other unexpected error.

```jsx
import React, { useState, useEffect } from "react";
import Axios from "axios";

default function Fetcher({ url }) {
  const [data, setData] = useState(null);

  useEffect(
    () => {
      // Set up a cancellation source
      let source = Axios.CancelToken.source();

      const loadData = async () => {
        try {
          const response = await Axios.get(url, {
            // Assign the source.token to this request
            cancelToken: source.token
          });
          setData(response.data);
        } catch (error) {
          // Is this error because we cancelled it ourselves?
          if (Axios.isCancel(error)) {
            console.log(`call for ${url} was cancelled`);
          } else {
            throw error;
          }
        }
      };
      loadData();

      return () => {
        // Let's cancel the request on effect cleanup
        source.cancel();
      };
    },
    [url]
  );

  if (!data) {
    return <div>Loading data from {url}</div>;
  }

  return <div>{JSON.stringify(data)}</div>;
}
```

### Effects with cleanup
There are some effects that require a cleanup to avoid memory leaks like subscriptions to external sources.

```jsx
import React, { useState, useEffect } from "react";

const MyComponent = () => {
  const [width, setWidth] = useState(window.innerWidth);
  
  useEffect(() => {
    const handleResize = () => setWidth(window.innerWidth);
    window.addEventListener("resize", handleResize);
    return () => window.removeEventListener("resize", handleResize);
  }, []);

  render() {
    return (
      <h1>{this.state.width}</h1>
    );
  }
}
```

As long as we only want our effect (subscribe to resizes) to be called once, we pass an empty array as the second parameter of the function useEffect.
An effect can optionally return a function (the cleanup function) that React will call when the component unmounts and before running the effect next time. In the example, our effect returns a function that unsubscribes it from the window resize events.

### Example with multiple effects
It’s always a good idea to use multiple effects to separate concerns. Below is an example of a component that is subscribed to window resizes (we do this with the first effect) and shows the type of screen we’re managing depending on its width (second effect).

```jsx
import React, { useState, useEffect } from "react";

const MyComponent = () => {
  const [width, setWidth] = useState(window.innerWidth);
  
  useEffect(() => {
    const handleResize = () => setWidth(window.innerWidth);
    window.addEventListener("resize", handleResize);
    return () => window.removeEventListener("resize", handleResize);
  }, []);
  
  useEffect(() => {
    const title = width < 400 ? "It's a phone" : "It's a pc";
    document.title = width;
    return () => document.title = "";
  }, [width]);

  render() {
    return (
      <h1>{width}</h1>
    );
  }
}
```