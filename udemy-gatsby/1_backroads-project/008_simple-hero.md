# Simple Hero

For now we'll do our setup just the basic way, and later with `graphql`. Let's start with our massove `Hero` component. It is shown on every page of our site. First lets create a new component `SimpleHero` in the `src/components`. 
We gonna be dealing with the massive background image, and we do wanna render something within the image. So, we need to use `{children}` props, otherwise nothing will be rendered. The `html` element will be the `header` and then within the `header` we ganna be rendering the children. In this case all the setup will be done with css. 
That's one of the way haw we can get images in React - is in fact using the css. 

**SimpleHero component**

```jsx
import React from 'react'

const SimpleHero = () => {
    return (
        <header className="defaultHero">{children}</header>
    )
}

export default SimpleHero;
```

Now we just want to decide where we wanna render this particular `SimpleHero`. So, we'll start with the `index.js` (home page). First we import `SimpleHero` to the `index.js` 

**index.js**
```jsx
import React from "react"
import {Link} from "gatsby"
import Layout from '../components/Layout'
import SimpleHero from '../components/SimpleHero'


export default () => {
   return (
    
       <Layout>
     
      <SimpleHero/>
   
       </Layout>
    
   ) 
} 
```
So, from where we get the `image` and the `styles`??? If we open our `layout.css` file we should have there `defaultHero` class. And there we are using the `url`(path) to grab our image from our `images` folder . 

```css
.defaultHero {
  min-height: calc(100vh - 62px);
  background: linear-gradient(rgba(63, 208, 212, 0.7), rgba(0, 0, 0, 0.7)),
    url("../images/defaultBcg.jpeg") center/cover no-repeat;
  display: flex;
  justify-content: center;
  align-items: center;
}
```

> But. There are multiple downsides of this way of using images, concerning optimization, sizes etc.  