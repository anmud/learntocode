# State Hook

`useState` is a Hook. We call it inside a `function component` to add some `local state` to it. `useState` returns a pair: the `current state value` (`count`) and a `function` that lets you update it (`setCount`).

```js
import React, { useState } from 'react';

function Example() {
  // Declare a new state variable, which we'll call "count"
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```

You can call this function from an event handler or somewhere else. The only argument to `useState` is the `initial state`. In the example above, it is `0` because our `counter` starts from zero. The initial state argument is only used during the first render.




