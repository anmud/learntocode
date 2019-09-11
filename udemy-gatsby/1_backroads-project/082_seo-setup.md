# SEO Setup

We'll add `head element` to all our `pages` where we'll provide information about the page, e.g 'title' and 'description'. We'll do that with a help of `react helmet` library - we'll use it to create a `component` that will control or add `metatags` in the `head element`; and then we gonna add this `component` to all our `pages`. 

Adding `metadata` will help search engins to better understand our `content`. 

First we'll install `gatsby-plugin-react-helmet` and add additional information to `gatsby-config`. 

And add the plugin to the plugins array in the `gatsby-config.js`

```js
plugins: [`gatsby-plugin-react-helmet`]
```

Next let's make some changes in the `site metadata` and add three properties to the object: twitterUserName, static image (we need to add it to our static folder), and siteUrl - the value for this property will be the url of our Netlify project. 

```js
 siteMetadata: {
    title: "BackRoads",
    description:
      "Explore awesome worldwide tours & discover what makes each of them unique. Forget your daily routine & say yes to adventure",
    author: "@anamo",
    twitterUsername: "@anmud",
    image: "defaultBcg.jpeg",
    siteUrl: "https://nostalgic-stonebraker-aeaf96.netlify.com",
  },
```




