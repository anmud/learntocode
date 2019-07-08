# Styling

There are a lot of variants: 

- complete css
- inline css
- global css
- file css
- css modules
- bootstrap
- gatsby config
- saas
- styled-components
- tailwind 
- .....

## Inline Styling

```jsx
import React from "react"
import {Link} from "gatsby"
import Layout from '../components/Layout'


export default () => {
   return (
    
       <Layout>
     
       <h1>Hello</h1>
       <Link to="/blog/">Blog</Link>
    
    <h1 style={{fontSize: '20px', textTransform: "capitalize", color: 'red'}}>
    hello styling
    </h1>
       </Layout>
    
   ) 
} 
```

## Global CSS

To use `global css` the better way is - `Layout component`. We create `CSS file` (layout.css) and then import it in the `Layout`. 

Here are 2 probleems: 

- the file will get bigger and bigger as the `application` grows - it will be too hard to maintain
- we must have unique `classNames`

## Component CSS

We can create css file for every component we have, e,g contact.css, blog.css, table.css, etc. 

The problems are almost the same:

- the file will get bigger and bigger as the `application` grows - it gets annoying 
- we must have unique `classNames`

## CSS Module

A `CSS Module` is a `CSS file` in which all class names and animation names are scoped locally by default.

`CSS Modules` let you write styles in CSS files but consume them as JavaScript objects for additional processing and safety. `CSS Modules` are very popular because they automatically make class and animation names unique so you don’t have to worry about selector name collisions.

**CSS Module example**

The CSS in a CSS module is no different than normal CSS, but the extension of the file is different to mark that the file will be processed.

```css

src/components/container.module.css

.container {
  margin: 3rem auto;
  max-width: 600px;
}
```
```jsx
src/components/container.js

import React from "react"
import containerStyles from "./container.module.css"

export default ({ children }) => (
  <section className={containerStyles.container}>{children}</section>
)
```

In this example, a CSS module is imported and declared as a JavaScript object called `containerStyles`. Then, a CSS class from that object is referenced in the `JSX className` attribute with `containerStyles.container`, which renders into HTML with dynamic CSS class names like `container-module--container--3MbgH`.

**When to use CSS Modules**

CSS Modules are highly recommended for those new to building with Gatsby (and React in general) as they allow you to write regular, portable CSS files while gaining performance benefits like only bundling referenced code.

## Bootstrap

For the Gatsby project we can install Bootstrap (npm install --save bootstrap), then we need just add the css from the bootstrap in css file of our component, in our case `layout.js`. 


```jsx
import React, {Fragment} from 'react'
import Navbar from '../components/Navbar'
import Footer from '../components/Footer'
import 'bootstrap/dist/css/butstrap.min.css'
// or import 'bootstrap/dist/css/butstrap.css'

const Layout = ({children}) => {
    return (
        <Fragment>
            <Navbar/>
            {children}
            <Footer/>
        </Fragment>
    )
}

export default Layout
```

Then in our `index.js` file (home page) we can use the styles. 

```jsx
import React from "react"
import {Link} from "gatsby"
import Layout from '../components/Layout'


export default () => {
   return (
    
       <Layout>
     
       <h1>Hello</h1>
       <Link to="/blog/">Blog</Link>

       <div className="container">
       <div className="row">
           <div className="col-4">Hello</div>
           <div className="col-4">Hello</div>
           <div className="col-4">Hello</div>
       </div>
       </div>
    
   
       </Layout>
    
   ) 
} 
```

## Gatsby Config and SASS

Here we'll need a `plugin`, and create `config file`.  So first we need to install `SASS plugin` from Gatsby plugin library - `npm install --save node-sass gatsby-plugin-sass`.

Then we need to create `gatsby-config.js` file.

**gatsby-config.js**

```jsx

module.exports = {
  plugins: [
     `gatsby-plugin-sass`,
      
  ]
}
```

Start the dev server. Then we create the folder inside the src and name it saas (`src/saas`), and in this folder we create the file (e.g. - `layout.scss`). We  also create a second file in the saas folder - `_variables.scss` - 

**_variables.scss**

```scss
$primaryColor: #f15025
```

Then we import this `variables.scss` file to our `layout.scss` file. 

**layout.scss**

```scss
@import './variables';

body{
   background: $primaryColor;
}
```

Then we import `layout.scss` into `layout.js` file

```jsx
import React, {Fragment} from 'react'
import Navbar from '../components/Navbar'
import Footer from '../components/Footer'
import '../saas/layout.scss'

const Layout = ({children}) => {
    return (
        <Fragment>
            <Navbar/>
            {children}
            <Footer/>
        </Fragment>
    )
}

export default Layout
```

We can combine SASS with  CSS Module. 


