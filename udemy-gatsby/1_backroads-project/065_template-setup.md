# Template Setup

Our `query`, that will be responsible for fetching information for each and every tour, is ready, now we can setup the `template`. And here we need to setup our `page query`. And the `data` with the `page query` we get in the `props`. 

**tour-template.js**

```jsx
import React from 'react'
import {graphql} from 'gatsby'

const Template = ({data}) => {
    return (
     <div>{data.tour.name}</div>
    )
}

export const query = graphql`
query($slug:String){
   tour:  contentfulTour(slug:{eq: $slug}){
      name
      price
      country
      days
      start(formatString: "dddd MMMM Do, YYYY")
      description{
        description
      }
      journey{
        day
        info
      }
      images{
        fluid{
          src
        }
      }
    }
  }
`

export default Template;
```

Let's destructure items we are gitting from the `data`, and **Note!** since a `description` is an object we need to look for the property of this object, so the syntax will differ a bit. And now we also can access `name` directly. 

**tour-template.js**

```jsx
import React from 'react'
import {graphql} from 'gatsby'

const Template = ({data}) => {

const {name, price, country, days, description:{description}, images, start, journey} = data.tour

    return (
     <div>{name}</div>
    )
}

export const query = graphql`
query($slug:String){
  tour:  contentfulTour(slug:{eq: $slug}){
      name
      price
      country
      days
      start(formatString: "dddd MMMM Do, YYYY")
      description{
        description
      }
      journey{
        day
        info
      }
      images{
        fluid{
          src
        }
      }
    }
  }
`

export default Template;
```

