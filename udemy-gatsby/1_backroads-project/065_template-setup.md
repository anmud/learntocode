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

Now let's render our images. We'll gonna use the destructuring with arrays, we would want to set up two more variables, first we gonna look for the first item in the array - first variable will be `mainImage`- and then in our destructuring we'll use rest operator - give us everithing else - all rest of the images that gonna be in this array, just collect it in the `tourImages` variable - and things that we've destructured we gonna set this equal to `images` array. 

`const [mainImage, ...tourImages] = images`

Now we can just loop over them and they will be displayed. And the main image we'll gonna pass in the `styledHero`.



