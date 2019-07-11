# Static Query

To use `StaticQuery` we first need to import it, the naming is important here. 
The difference here - we also need to return it as a `component`. 

**RegularHeader.js**

```jsx
import React from "react"
import {StaticQuery} from "gatsby"
import { graphql } from "gatsby"

const RegularHeader = () => {
  
    return (
        <div>
           <StaticQuery></StaticQuery>
        </div>
    )
}

export default RegularHeader; 
```

There are two more `props` tha we would need to include whaen we wanna use `StaticQuery`: `query prop` - where we'll pass our `query` (we can onclude qraphql in the prop, or use external variable), and second - a `render prop`. 

> If we are using the `query keyword` and have the `name` of the `query` make sure that names of dirrerent queries are unique, cos the names are global, so if we run the same query with the sane name it will fail. 

**RegularHeader.js**

```jsx
import { graphql } from "gatsby"


const RegularHeader = () => {

   const getSiteData = graphql`
   query{
       site{
         siteMetadata{
           title
           description
           author
         }
       }
     }
   `
  
    return (
        <div>
           <StaticQuery query={getSiteData} render={}/>
        </div>
    )
}


export default RegularHeader; 
```
The `render prop` is interesting - cos in the `render prop` we are passing the `function` . The `first argument` in the `function` will be the `data`, that we are getting back. And we are making return from this particular `function`. Then we can deside how we can access it: either using destructuring above the `return` or use the long way, naming all the properties from the `data object`.

**RegularHeader.js** without destructuring 

```jsx
import React from "react"
import {StaticQuery} from "gatsby"
import { graphql } from "gatsby"

const RegularHeader = () => {

   const getSiteData = graphql`
   query{
       site{
         siteMetadata{
           title
           description
           author
         }
       }
     }
   `
  
    return (
        <div>
           <StaticQuery query={getSiteData} render={(data) => {
               return <div>
                   <h1>{data.site.siteMetadata.description}</h1>
                   </div>
           }}/>
        </div>
    )
}


export default RegularHeader; 
```
