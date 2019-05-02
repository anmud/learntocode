# Review: Lifecycle Methods on Class-based Components 

The purpose of the `useEffect` Hook is to offer similar functionailty to what `lifecycle methods` offer in `class-based` components, but in our new `functional components`. 

What is a `lifecycle method`? A `lifecycle method` is a `function` that runs at a certain point of the existence of a `class-based` React component. For example, there are `lifecycle methods` that run when a `component` is first mounted, when it it unmounted or removed from the DOM, as well as after updates: for example, a fresh re-render due to new `state` or new props.  

Let's begin with `componentDidMount` and `componentDidUpdate`.
The `componentDidMount` lifecycle method is invoked when the `component` is first mounted to the DOM. The `componentDidUpdate` lifecycle method is invoked after the DOM update or anotherwords after the `component` re-renders. 

Let's have look at this in the context of a classic `class-based` counter app.

```jsx
import React, {Component} from 'react';

class App extends Component {
  constructor(props){
   super(props);
   this.state = {
       count: 0,
   }
  }

 componentDidMount(){
     console.log('This is componentDidMount. I run after the initial render')
 }

 componentDidUpdate(prevProps, prevState){
  console.log('This is componentDidUpdate. I run after any subsequent render')
 }

  render(){
      const {count} = this.state
      return (
    <div>
      <button onClick={()=> this.setState({count: count + 1})>Increase</button>
      <button onClick={()=> this.setState({count: count 1 1})>Decrease</button>
      <h1>{count}</h1>
    </div>
  );
  }
  
}

export default App;
```
The last `lifecycle method` to discuss is `componentWillUnmount` which is invoked right before the `component` is removed from the DOM, right before it dissapeares from the view. 

In terms of `component design` the standart proptocol works like this: 
- The `componentDidMount` lifecycle method sets at the component to be used. E.g typically in `componentDidMount` we  can do smth. like making a request to the `API` for `data`, or setup a `subscription` or create any `event listeners`. 
- After we do that in the `componentWillUnmount` lifecicle method those initial subscriptions and event listners are torn down. This method is ment to reverse everything we setup in `componentDidMount`. It's for this reason that `setState` method is never actually called or should not be called in `componentWillUnmount`. The reason for that is, of course, is because the `component` is about to be removed, it's not gonna be rerendered, so we don't wanna modify `state` on the `component` that will not exist in a few moments. 

To show this let's have two components: `Counter component` and `App component`. What we wanna do is that `App component` conditionally renders `Counter component`. 

##### Counter Component
```jsx
import React, {Component} from 'react';

class Counter extends Component {
  constructor(props){
   super(props);
   this.state = {
       count: 0,
   }
  }

 componentDidMount(){
     console.log('This is componentDidMount. I run after the initial render')
 }

 componentDidUpdate(prevProps, prevState){
  console.log('This is componentDidUpdate. I run after any subsequent render')
 }

 componentWillUnmount(){
     console.log('This is componentWillUnmout. Hey I am about to be removed')
 }

  render(){
      const {count} = this.state
      return (
    <div>
      <button onClick={()=> this.setState({count: count + 1})>Increase</button>
      <button onClick={()=> this.setState({count: count 1 1})>Decrease</button>
      <h1>{count}</h1>
    </div>
  );
  }
  
}

export default Counter;
```
##### App component
```jsx
import React, {Component} from 'react';

class App extends Component {
  constructor(props){
   super(props);
   this.state = {
       visible: false,
   }
  }

 

  render(){
      const {visible} = this.state
      return (
    <div>
     <button onClick={() => this.setState({visible: !visible})}>
        Show / Hide the Counter Component
     </button>

     {visible && <Counter/>}
    </div>
  );
  }
  
}

export default App;
```