# CSS fix

Even though we are working with `CSS Modules` (and they are awesome), we do need to remember that only the `classNames` are being lockaly scoped. 

Let's say in our `error.module.css` by mistake we gonna select something globally (this could be by mistake, or we could purposly do that).

**error.module.css**
```css
.error {
  background: var(--primaryColor);
  min-height: calc(100vh - 62px);
  display: flex;
  justify-content: center;
  align-items: center;
}

/* "a" is selected globally */
a{
 font-size: 4rem;
}
```
> Then we'll have the issue actually when all the `links` all around our `site` will also be changed !!!!!! Cos we are not scoping this locally. 

This is something that we need to keep an eye on. 

There are some solutions:

- either we will be using SAAS
- or in the `module.css` files we will use the `className` and then select the element

```css
.banner h1 {
  font-size: 3.3rem;
  text-transform: uppercase;
  margin-bottom: 2rem;
  padding: 0 1rem;
  letter-spacing: 6px;
}
```
- or we'll use `classNames` for every element


Let's imagine the scenario when we wanna our `footer` sittind all the way in the bottom. Of course, if we gonna be adding more content it will fix by itself, but let's say as we are currently working with the project we still wanna see or footer rendered down to the bottom. 

We can fix that using the magic of the `flexbox`. In our `Layout.js` we'll create `<main>` element instead of just having a regular `Fragment`. 

**Layout.js**
```jsx
import React, {Fragment} from 'react'
import Navbar from '../components/Navbar'
import Footer from '../components/Footer'
import './layout.css'

const Layout = ({children}) => {
    return (
        <main>
            <Navbar/>
            {children}
            <Footer/>
        </main>
    )
}

export default Layout
```
Then in the `layout.css` we'll add some styling to our `main` element: `min-height` of 100% (even though it is not enough content - it will always be 100% of the view); `display: flex` (it will be a flexbox); by default it will be flexbow row, to make it a column we need `flex direction` and set this up as a `column`. We would need to head over to the `footer.css`. And in the `footer` the main class we add `margin-top: auto` - it will push `footer` down to the bottom. 

layout.css
```css
main{
  min-height: 100vh;
  display: flex; 
  flex-direction: column
}
```

footer.css
```css
.footer {
  margin-top: auto;
  background: var(--mainBlack);
  padding: 2rem;
  text-align: center;
  color: var(--mainWhite);
}
```