# Alternate Syntax

What `styled components` offer us - instead of the case where we do have the `component` and thin within this `component` we have `styled components` and then we are exporting the `React component`  - we can set this up as `export default` and instead of exporting the `Title` we can in fact setup `styled components` where instead of using `html element` we will use the `React component` itself. The syntax will be almost the same. 

We don't need `TitleWrapper` anymore, and we need one more `prop` (className) as well. And then we need to use the same `className` for the `<div>` and set this equal to the `className prop` (- that we are getting form our Title component).

**Title.js**

```jsx
import React from 'react'
import styled from 'styled-components'

const Title = ({title, subtitle, className}) => {
   return (
       <div className={className}>
           <h4>
               <span className="title">{title}</span>
               <span>{subtitle}</span>
           </h4>
      </div>
   )
}

export default styled(Title)`    //we export here
   text-transform: uppercase;
   font-size: 2.3rem;
   margin-bottom: 2rem;
   h4{
       text-align: center;
       letter-spacing: 7px;
       color: var(--primaryColor); 
   }
   .title{
       color: var(--mainBlack)
   }
   span{
       display: block;
   }
   @media (min-width:576px){
       span{
           display: inline-block;
           margin: 0 0.35rem;
       }
   }
`

export default Title;
```