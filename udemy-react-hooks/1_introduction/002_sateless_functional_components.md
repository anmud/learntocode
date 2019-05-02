# Review - Stateless functional components

The `hooks` combine best features of both: `functional components` and `class-based-components`. Well, a `component` is just a `container` of one or more `visual elements` that forms part of our `DOM`, our `view`, part of the `user interface` that we see and interact with. 

`Components` may or may not have smth. called `state`. `State` refers to a component's `data`, and `data` may also change over time. Not all `components` need to have `state`, not all `components` need to have `data`. The part of the `view` that a `component` represents may just be static and fixed, unchanging. One of the examples is the `footer`, the `footer` is just a collection of `links`, it doesn't involve any custom information. 

- So, if it's just a bunch of whole random `html` that we want to represent, a `sateless functionl component` is the best way to do it. 
- If a `component` itsn't keeping track of any kind of `internal state` or `data` and just need to represent something visual - a `sateless component` shows the most light way that we can accomplish that. 

`Stateless functional component` :

It's `sateless` cos it doesn't have any `state`. And it a `functional component` cos it's created by a plain `js function`. 

```jsx
import React from 'react';


const App = () => {
  return (
    <div>
      <h1>Welcome to the app</h1>
    </div>
  );
}

export default App;
```

#### Props 
If we think of a `react component` as a `function`, `the props` represent the `arguments` to that `function`; the other way to think about `props` - they are `inputs` that passed into a `component`, that a `component` can use either in its `business logic` or in its actual `rendered output`. More specifically `props` are inputs that are passed to a `component` from its `parent`. And its `parent` is a `componenet` that renders that. 

##### App component
```jsx
import React from 'react';

const App = () => {
  return (
    <div>
      <Box text="Hi, Ana"/>
    </div>
  );
}

export default App;
```

##### Box component
```jsx
import React from 'react';


const Box = (props) => {
  return (
    <div>
      <h1>{props.text}</h1>
    </div>
  );
}

export default Box;
```

`props` here in the `Box component` is gonna be a js `object` that's going to store all of the `props` as the `properties of the object`.

1. we are creating a `react component` called `App`.
2. within `App` we are rendering another `Box` component, and we are giving the `Box` component a `prop` called `text` and the value for the prop
3. then `Box` component recieves the `prop` in a single `object` and we are able in the `Box` component access the `props`.

We are not limited to just one `prop` we cann pass as many as we want. 