# Title Component

In our `components` folder let's create one more folder ("Home"). We'll do this cos there will be some `components` that we will be using globally - all through out the project. However, there are `sections` and/or `components` that will be specific only for the `home page` or only for the `tours page` let's say. 
It will be useful if we'll create a separate folder where all the `components` that let's say we gonna be using for the `home page` will be stored. 

So, in the `components/home` let's create "About.js" file. And setup the `title component` which will be use globally. We'll create the `title component` in the components folder, but we wanna render it in the `About section`. 

The idea is simple - if we know that we wanna use the `styled title component` in all the `sections` we would like to setup some kind of placeholder for that `section`. 

**components/title**

```jsx
import React from 'react'

const Title = () => {
   return (
       <div>
           
       </div>
   )
}

export default Title;
```

And import our `title component` to our `about section` 

**components/home/about**

```jsx
import React from 'react'
import Title from '../Home/About'


const About = () => {
    return (
      <div>
      <Title/>
      </div>
    )
}

export default About;
```

And then, at the very least we would need to import it in one of  the `pages` also. So, in our `index.js` (which is our home page of the site), we'll import the `About section`. 

**index.js**

```jsx
import React from "react"
import {Link} from "gatsby"
import Layout from '../components/Layout'
import SimpleHero from '../components/SimpleHero'
import Banner from '../components/Banner'
import About from '../components/Home/About'



export default () => {
   return (
    
       <Layout>
     
      <SimpleHero>
        <Banner  
        title="Some Title"  
        info="Lorem ipsum dolor sit amet, consectetur adipiscing elit,  
        sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.">
          <Link to="/tours" className="btn-white">explore tours</Link>
        </Banner>
      </SimpleHero>

      <About/>
     
       </Layout>
    
   ) 
} 
```
Now we continue working with the `styled Title` component. First we'll set this up using two `props` (title and subtitle => our title has two separate words, so that's why we have two props) and use them just for the styling. 

**Title.js**

```jsx
import React from 'react'

const Title = ({title, subtitle}) => {
   return (
       <div>
           hello from title
       </div>
   )
}

export default Title;
```

Then in our `<div>` we'll have `<h4>` element with the two `<span>`'s whithin. 

**Title.js**

```jsx
import React from 'react'

const Title = ({title, subtitle}) => {
   return (
       <div>
           <h4>
               <span className="title">{title}</span>
               <span>{subtitle}</span>
           </h4>
       </div>
   )
}

export default Title;
```

Now we should pass these two `props` to the `Title.js` components. So, we go to our `About` component where our `Title` is rendered and pass the `props`. 

**About.js**

```jsx
import React from 'react'
import Title from '../Title'


const About = () => {
    return (
      <div>
       <Title title="about" subtitle="us"/>
      </div>
    )
}

export default About;
```

So, now is the time to set our styling. First we import `styled components` to the `Title.js`. Let's start from the basic one - transfer the simple `<div>` to the `styled components` `<div>`. We need somw kind of naming here - the first one will be `TitleWrapper`, inside the styled `<div>` we can setup the styles we need. First of all we need to delete the simple `<div>` and use the `TitleWrapper` instead. 

So, in this case we use out actual `React component` and use `styled components` just for stylyng the elements. 

**Title.js**

```jsx
import React from 'react'
import styled from 'styled-components'

const Title = ({title, subtitle}) => {
   return (
       <TitleWrapper>
           <h4>
               <span className="title">{title}</span>
               <span>{subtitle}</span>
           </h4>
       </TitleWrapper>
   )
}

const TitleWrapper = styled.div`
  text-transform: uppercase;
   font-size: 2.3rem;
   margin-bottom: 2rem;
   
`

export default Title;
```

What is cool about the `styled components` that straight out of the box we can do the `nesting`, so we can style the `<h4>` inside the `TitleWrapper`.
More than that we have access to any classes that we have. On our `<span>` we have the `className` "title", so we can also style it within the `TitleWrapper`.  

**Title.js**

```jsx
import React from 'react'
import styled from 'styled-components'

const Title = ({title, subtitle}) => {
   return (
       <TitleWrapper>
           <h4>
               <span className="title">{title}</span>
               <span>{subtitle}</span>
           </h4>
       </TitleWrapper>
   )
}

const TitleWrapper = styled.div`
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
`

export default Title;
```

We just add the `display: block` so that our `<span>`'s were sitting one under another, and we also need `media query` - in the `styled components` they have a little bit different syntax. 

**Title.js**

```jsx
import React from 'react'
import styled from 'styled-components'

const Title = ({title, subtitle}) => {
   return (
       <TitleWrapper>
           <h4>
               <span className="title">{title}</span>
               <span>{subtitle}</span>
           </h4>
       </TitleWrapper>
   )
}

const TitleWrapper = styled.div`
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

So, now we can reuse this `styled Title` component all over the page. 