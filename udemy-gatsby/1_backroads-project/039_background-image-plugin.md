# Background Image Plugin

We also can setup a `plugin` for the `background images`, cos they also could use all the optimisations. In order to do that we need to install the `gatsby-background-image` plugin first - `npm install --save gatsby-background-image`. And restart the server. 

Well, we would like to customise the image we use, so to use it in different pages and in different sizes and styling. Now let's create a new `component` named "StyledHero.js". For this `component` we first import `styled components` and `background image` plugin. 

**StyledHero.js**

```jsx
import React from 'react'
import styled from 'styled-components'
import BackgroundImage from 'gatsby-background-image'

const StyledHero = () => {
  <div>

  </div>
}

export default StyledHero;
```

Well, we would like to reuse this `component` all thoughout the pages of our project. The way we gonna do that - we'll setup a bunch of `props` for the `component` - cos we also would like to change the `image` of this `component` depending on the page we are locaked at. 
Props will be: `img` - the image that will be rendered, `className` , `children` - cos we wanna render our `banner` on the `image`, `home` - this prop will be responsible for two things: whether the `image` will gonna have the `linear gradient` as well as the size of the image, if there will be no `home prop` then the image will be smaller and there will not be `linear gradient`.

And we would like to return in the `component` the - `BackgroundImage`. 

**StyledHero.js**

```jsx
import React from 'react'
import styled from 'styled-components'
import BackgroundImage from 'gatsby-background-image'

const StyledHero = ({img, className, children, home}) => {
  <BackgroundImage>

  </BackgroundImage>
}

export default StyledHero;
```

The reason why we add a `className` as a prop -  cos we will be exporting the `component` setup as `styled component`. If in the `styled componnets` we pass the actual `react component` then we do need to use the `className` prop. And before we work on our `css` we will render the `children` - they will be rendered within the `BackgroundImage` component. 

**StyledHero.js**

```jsx
import React from 'react'
import styled from 'styled-components'
import BackgroundImage from 'gatsby-background-image'

const StyledHero = ({img, className, children, home}) => {
  <BackgroundImage className={className}>
    {children}
  </BackgroundImage>
}

export default styled(StyledHero);
```

What we are doing with the `img` prop? Our `BackgroundImage` component will be looking for this prop (whether fluid or fixed) and the `value` of this prop will be the `data` we are getting from the `query`. But in our case we are not gonna setup the `query` inside the `component` - in fact for each and every page we gonna pass the `img prop`. And we also pass `home prop`. 

**StyledHero.js**

```jsx
import React from 'react'
import styled from 'styled-components'
import BackgroundImage from 'gatsby-background-image'

const StyledHero = ({img, className, children, home}) => {
  <BackgroundImage className={className} fluid={img} home={home}>
  {children}
  </BackgroundImage>
}

export default styled(StyledHero)`


`
```

 Now, let's work on the styling: background position, size, opacity, display...
 Concerning the `home prop` - when we are dealing with `styled components` we have an option when we can do `conditional rendering`, cos `styled components` within the tagged template function, we can use interpolations and we have few options: use regular `string` or use the `props`. 
First let's deal with `linear gradient`, first we'll add `background` and setup a conditional rendering with the `ternary operator`. The same we'll do with the `height`.

**StyledHero.js**

```jsx
import React from 'react'
import styled from 'styled-components'
import BackgroundImage from 'gatsby-background-image'

const StyledHero = ({img, className, children, home}) => {
  <BackgroundImage className={className} fluid={img} home={home}>
  {children}
  </BackgroundImage>
}

export default styled(StyledHero)`
 min-height: ${props => props.home ? "calc(100vh - 62px)" : "50vh"}
 background: ${props => props.home ? "linear-gradient(rgba(63, 208, 212, 0.7), rgba(0, 0, 0, 0.7))" : "none"};
 background-position: center;
 background-size: cover;
 opacity: 1 !important;
 display: flex;
 justify-content: center;
 align-items: center; 
`
```