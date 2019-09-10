# Single Blog Query

Once we have our template for our pages we need to setup each blog page. We remember that we are passing the `slug` variable within the `createPages` function in `gatsby-node` file. Now in our `blog template` 
we need to setup the query and use this variable as an argument. 

As far as for the post we've setup `rich text` content field we should ask in the query for the `json` format as a response.

```js
query getPost($slug:String){
  post: contentfulPost(slug: {eq: $slug}){
    title
    published
    text{
      json
    }
  }
}
```


