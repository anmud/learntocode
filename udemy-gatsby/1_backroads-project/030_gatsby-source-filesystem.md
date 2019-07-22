# Gatsby source filesystem

 We now know three possible way of getting `data`in gatsby. To render images we need to install an additional plugin - `gatsby-source-filesystem`.

 When the plugin is installed we'll have access to two fields: one of them will be  `allFile` that will return files from our specific directory that we'll gonna select; and a second one will return a `single file` from that particular directory. 

 How do we work with this plugin? First we'll have to add it in our `config` file as an object. In fact we can use this plugin to use for multiple sources. So, in the object we have the `propery` by the name of `resolve`- the `value`of this property needs to be the name of that particular plugin (in our case "gatsby-source-filesystem").  Then for this particular plugin we'll gonna have `options object` within which we have two more properties: **name** - the name is up to you, this is your reference to know how will you name the source that you'll be getting ; **path** - just gives the path to that particular folder where you'll gonna be looking for your sources, however since this is the node.js file they use `__dirname` - and this will return the path of the folder where the current js file is locted. 

** gatsby-config.js**

 ```jsx
 module.exports = {
  siteMetadata: {
    title: "Backroads",
    description: "Explore awesome worldwide tours and discover what makes each of them unique. Forget your daily routine & say yes to adventure",
    author: '@anmud',
  
  },
  plugins: [
    {
      resolve: `gatsby-source-filesystem`,
      options: {
        name: `images`,
        path: `${__dirname}/src/images`,
      },
    },
    `gatsby-plugin-styled-components`,
      
  ],
}
```

Now we need to restart the server. Once this have done we have access to these fields in the `qraphiQL` interface. 
