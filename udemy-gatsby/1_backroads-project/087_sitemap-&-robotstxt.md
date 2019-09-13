# Sitemap and Robots.txt

First we need to install additional plugins: sitemap - provides information about pages, videos and other files on our site and relationships between them; robots.txt will give instructions to the robots about the pages. After installing we need to update the `config` file and restart the server. 

**gatsby-config**

```jsx
require("dotenv").config({
  path: `.env.${process.env.NODE_ENV}`,
})
module.exports = {
  siteMetadata: {
    title: "BackRoads",
    description:
      "Explore awesome worldwide tours & discover what makes each of them unique. Forget your daily routine & say yes to adventure",
    author: "@anmud",
    twitterUsername: "@anmud_mo",
    image: "/static/defaultBcg.jpeg",
    siteUrl: "https://nostalgic-stonebraker-aeaf96.netlify.com",
  },
  plugins: [
    `gatsby-plugin-react-helmet`,
    `gatsby-plugin-sitemap`,
    {
      resolve: 'gatsby-plugin-robots-txt',
      options: {
        host: 'https://nostalgic-stonebraker-aeaf96.netlify.com',
        sitemap: 'https://nostalgic-stonebraker-aeaf96.netlify.com/sitemap.xml',
        policy: [{ userAgent: '*', allow: '/' }]
      }
    },
    {
      resolve: `gatsby-source-filesystem`,
      options: {
        name: `images`,
        path: `${__dirname}/src/images/`,
      },
    },
    {
      resolve: `gatsby-source-contentful`,
      options: {
        spaceId: process.env.CONTENTFUL_SPACE_ID,
        accessToken: process.env.CONTENFUL_ACCESS_TOKEN,
      },
    },
    `gatsby-transformer-sharp`,
    `gatsby-plugin-sharp`,
    `gatsby-plugin-styled-components`,
    `gatsby-plugin-transition-link`,
    `gatsby-plugin-playground`,
  ],
}

```