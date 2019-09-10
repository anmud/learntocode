# Pagination setup

Let's first setup the query -  a query that will be used for every page. First we need to do some `sorting` according to the published date. Also we could `limit` how many posts we gonna be having, each query will have different `limit` number. For pages number two, three and so on will use also `skip` argument, so that we have specific posts on the page, namely we can skip first five posts and render the next on the page number two, then we can skip e.g ten and render the last on the third page.

So for the pages with pagination will create one more `template`. Important here that in our `gatsby-node.js` file we'll need to pass more `variables` in the `context` - for limit, skip and sort -, because our `template` will be responsible for displaying a list of posts. 

```js
query getPosts($skip:Int, $limit:Int){
  posts: allContentfulPost(skip:$skip, limit:$limit, sort: {fields: published, order: DESC}){
    edges{
      node{
        slug
      }
    }
  }
}
```

Next we'll create separate pages and for every page we gonna run this `query`. The `values` for the `variables` will come from gatsby node.



