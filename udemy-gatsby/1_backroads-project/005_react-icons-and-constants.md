# React Icons and Constants

We'll use for the project not the Gatsby specific but react spesific plugin. 
Install - `npm install --save react-icons`.

[documentation for the plugin](https://react-icons.netlify.com/#/)

- The end result will be SVG by default
- we have multiple icin libraries available

**Installation**
`npm install react-icons --save`

**Usage**
```jsx
import { FaBeer } from 'react-icons/fa'; //the name of the libtrary and the name of the icon we use

class Question extends React.Component {
  render() {
    return <h3> Lets go for a <FaBeer />? </h3>
  }
}
```

### Constants

By `constants` in this project we mean a separate folder with the links, social icons and services we'll use in our site. So, in this folder we;ll have three separate files: `links`, `services` and `social icons`. 

> **Note** This is not specific to `Gatsby`. We can use it for any `React` project. 

**links.js**

```jsx
export default [
  {
    path: "/",
    text: "home",
  },
  {
    path: "/tours",
    text: "tours",
  },
  {
    path: "/blog",
    text: "blog",
  },
  {
    path: "/contact",
    text: "contact",
  },
]
```

**services.js**

```jsx
import React from "react"
import { FaWallet, FaTree, FaSocks } from "react-icons/fa"

export default [
  {
    icon: <FaWallet />,
    title: "saving money",
    text:
      "Lorem ipsum, dolor sit amet consectetur adipisicing elit. Obcaecati, earum. ",
  },
  {
    icon: <FaTree />,
    title: "endless hiking",
    text:
      "Lorem ipsum, dolor sit amet consectetur adipisicing elit. Obcaecati, earum. ",
  },
  {
    icon: <FaSocks />,
    title: "amazing comfort",
    text:
      "Lorem ipsum, dolor sit amet consectetur adipisicing elit. Obcaecati, earum. ",
  },
]
```

**social-icons.js**

```jsx 
import React from "react"
import { FaFacebook, FaTwitterSquare, FaSquarespace } from "react-icons/fa"
export default [
  {
    icon: <FaFacebook />,
    url: "https://twitter.com/?lang=en",
  },
  {
    icon: <FaTwitterSquare />,
    url: "https://twitter.com/?lang=en",
  },
  {
    icon: <FaSquarespace />,
    url: "https://twitter.com/?lang=en",
  },
]
```


