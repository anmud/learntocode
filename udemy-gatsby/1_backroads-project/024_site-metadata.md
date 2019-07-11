# Site Metadata

Before writing `query` we need to deside what kind of `data` we'll be requesting. Our first main goal will be getting `images`, so we can use `gatsby-image-plugin` for optimisations. 

But in order to `query` images we have to install few more plugins. So, for now let's start simple and just ask for the `sate metadata`. 

In the `gatsby-cofig.js` file we gonna have to create a `key-value pair` - `siteMetadata`; **the naming here IS important**.

**gatsby-config.js**

```js
module.exports = {
  siteMetadata: {
    title: "Backroads",
    description: "Explore awesome worldwide tours and discover what makes each of them unique. Forget your daily routine & say yes to adventure",
    author: '@anmud',
  },
  plugins: [
    
    `gatsby-plugin-styled-components`,
      
  ],
}
```

> Important here - the moment we created these properties, we need to restart the `gatsby development` server. 
> If we do any kind of cjanges to `gatsby-config` file we do neet to restart the development server. 
> For the detailed information always use [gatsby config docs](https://www.gatsbyjs.org/docs/gatsby-config/)


The exception would be - within the `siteMetadata` object we can add whatever propery we would like, e.g "data". 

**gatsby-config.js**

```js
module.exports = {
  siteMetadata: {
    title: "Backroads",
    description: "Explore awesome worldwide tours and discover what makes each of them unique. Forget your daily routine & say yes to adventure",
    author: '@anmud',
    data: ["item1", "item2"]
  },
  plugins: [
    
    `gatsby-plugin-styled-components`,
      
  ],
}
```

However if we add some properies, that not supposed to be in the main object, to the main object (module.exports) - we'll get an error. 


