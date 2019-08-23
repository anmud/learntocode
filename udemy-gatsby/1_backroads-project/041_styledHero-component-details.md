# Adding Background Images to All Pages

There are three more pages where we wanna add `background images` as well - "Tours", "About" and "Contact". For all of them we would need to import `graphql` and `StyledHero` Component, and use the same query to get the `image`. 

**tours.js**

```jsx
import React from 'react'
import Layout from '../components/Layout'
//import Header from '../examples/Header'
import RegularHeader from '../examples/RegularHeader'
import StyledHero from '../components/StyledHero'
import {graphql} from 'gatsby'


const Tours = ({data}) => {

    const image = data.connectBcg.childImageSharp.fluid

    return (
        <Layout>
            <StyledHero image={image}>
            <p>hello from tours</p>

           <RegularHeader/>

           {/* <Header/> */}
            </StyledHero>
           
        </Layout>
    )
}

export default Tours;

export const query = graphql`
query{
  connectBcg: file(relativePath: {eq:"connectBcg.jpeg"}){
    childImageSharp{
      fluid(maxWidth:4160, quality: 90){
        ...GatsbyImageSharpFluid_withWebp
      }
    }
  }
}
`
```

The same will do with the other components, just changing the image we need. 