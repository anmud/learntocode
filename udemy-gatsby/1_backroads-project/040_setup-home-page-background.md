# Setup Home Page Background

For our homa page we now wanna use the `StyledHero` we just created.

```jsx
import React from "react"
import {Link} from "gatsby"
import Layout from '../components/Layout'
import StyledHero from '../components/StyledHero'
import Banner from '../components/Banner'
import About from '../components/Home/About'
import Services from '../components/Home/Services'



export default () => {
   return (
    
       <Layout>
     
      <StyledHero>
        <Banner  
        title="Some Title"  
        info="Lorem ipsum dolor sit amet, consectetur adipiscing elit,  
        sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.">
          <Link to="/tours" className="btn-white">explore tours</Link>
        </Banner>
      </StyledHero>

      <About/>
      <Services/>
     
       </Layout>
    
   ) 
} 
```

Now we need to pass an `image` to our `StyledHero` component. In order to access the `image` we first need to setup the `query`.

```js

`query{
  defaultBcg: file(relativePath: {eq:"defaultBcg.jpeg"}){
    childImageSharp{
      fluid(quality:90, maxWidth:4160){
         ...GatsbyImageSharpFluid_withWebp
      }
    }
  }
}`
```
 Actually we gonna setup a `page query` the reason for that is - for each page we wanna have a different `image`. So we'll need {qraphql} import.  

 **index.js**

 ```jsx
 import React from "react"
import {Link} from "gatsby"
import Layout from '../components/Layout'
import StyledHero from '../components/StyledHero'
import Banner from '../components/Banner'
import About from '../components/Home/About'
import Services from '../components/Home/Services'
import {graphql} from 'gatsby'



export default () => {
   return (
    
       <Layout>
     
      <StyledHero >
        <Banner  
        title="Some Title"  
        info="Lorem ipsum dolor sit amet, consectetur adipiscing elit,  
        sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.">
          <Link to="/tours" className="btn-white">explore tours</Link>
        </Banner>
      </StyledHero>

      <About/>
      <Services/>
     
       </Layout>
    
   ) 
} 

export const query = graphql`
query{
  defaultBcg: file(relativePath: {eq:"defaultBcg.jpeg"}){
    childImageSharp{
      fluid(quality:90, maxWidth:4160){
         ...GatsbyImageSharpFluid_withWebp
      }
    }
  }
}
`
```

> Remember with `page queries` we should have access to the `data` so we pass it as an argument for the `index.js` component. 

 **index.js**

 ```jsx
 import React from "react"
import {Link} from "gatsby"
import Layout from '../components/Layout'
import StyledHero from '../components/StyledHero'
import Banner from '../components/Banner'
import About from '../components/Home/About'
import Services from '../components/Home/Services'
import {graphql} from 'gatsby'



export default ({data}) => {   //access data here
   return (
    
       <Layout>
     
      <StyledHero>
        <Banner  
        title="Some Title"  
        info="Lorem ipsum dolor sit amet, consectetur adipiscing elit,  
        sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.">
          <Link to="/tours" className="btn-white">explore tours</Link>
        </Banner>
      </StyledHero>

      <About/>
      <Services/>
     
       </Layout>
    
   ) 
} 

export const query = graphql`
query{
  defaultBcg: file(relativePath: {eq:"defaultBcg.jpeg"}){
    childImageSharp{
      fluid(quality:90, maxWidth:4160){
         ...GatsbyImageSharpFluid_withWebp
      }
    }
  }
}
`
```

Now the `data` we gat from our query we can use to render the `image`, in our case we'll pass it as a `prop` to the `StyledHero` component. We also have `home={true}` prop where we could setup whatever size we would like. 

**index.js**

```js
import React from "react"
import {Link} from "gatsby"
import Layout from '../components/Layout'
import StyledHero from '../components/StyledHero'
import Banner from '../components/Banner'
import About from '../components/Home/About'
import Services from '../components/Home/Services'
import {graphql} from 'gatsby'



export default ({data}) => {

  const image = data.defaultBcg.childImageSharp.fluid

   return (
    
  
       <Layout>
     
      <StyledHero home={true} image={image}> //pass prop here 
        <Banner  
        title="Some Title"  
        info="Lorem ipsum dolor sit amet, consectetur adipiscing elit,  
        sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.">
          <Link to="/tours" className="btn-white">explore tours</Link>
        </Banner>
      </StyledHero>

      <About/>
      <Services/>
     
       </Layout>
    
   ) 
} 

export const query = graphql`
query{
  defaultBcg: file(relativePath: {eq:"defaultBcg.jpeg"}){
    childImageSharp{
      fluid(quality:90, maxWidth:4160){
        ...GatsbyImageSharpFluid_withWebp
      }
    }
  }
}
`
```

