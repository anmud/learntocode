# Review - Class-based-components

Passing `props` with the syntaxt of `class-based-components` 

#### Button component
```jsx
import React, {Component} from 'react';


class Button extends Component {
  constructor(props){
   super(props);
   this.state = {
    activated: false
   }
   this.handleActiveChange = this.handleActiveChange.bind(this);
  }


handleActiveChange(){
   // this.setState({activated: !this.state.activated})
   this.setSate((prevState)=> {
       return {
           activated: !prevState.activated
       }
   })
}

  render(){
      const buttonText = this.state.activated ? this.props.activeText : this.props.inactiveText
      return (
    <div>
      <button onClick={this.handleActiveChange}>{buttonText}</button>
    </div>
  );
  }
  
}

export default Button;
```

#### App component 

```jsx
import React, {Component} from 'react';


class App extends Component {
  render(){
      
      return (
    <div>
      <Button  
       activeText = "ON"
       inactiveText = "OFF
      />
    </div>
  );
  }
  
}

export default App;
```