# Error Page

If we go to some kind of `url` that doesn't exist we wanna have our `Error page` rendering. We need to create a `component` and the `css` file for the `component`. 
In our `Error` page we can use the `Banner` which we created for the `SimpleHero`, and just change the props. 

**404.js**
```jsx
import React from 'react'
import Layout from '../components/Layout'
import styles from '../css/error.module.css'
import {Link} from 'gatsby'
import Banner from '../components/Banner'

const Error = () => {
  return (
      <Layout>
         <header className={styles.error}>
          <Banner title="oops it's a dead end">
            <Link to="/" className="btn-white">
              back to home page
            </Link>
          </Banner>
         </header>
      </Layout>
  )
}

export default Error;
```