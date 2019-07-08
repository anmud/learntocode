# Layout Component

When we are aetting out the `Layout` component, we need to make sure that we are useng the `{children}` prop; that will make sure that everything that will be in the `Layout` will be rendered. 

```jsx
import React, {Fragment} from 'react'
import Navbar from '../components/Navbar'
import Footer from '../components/Footer'

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