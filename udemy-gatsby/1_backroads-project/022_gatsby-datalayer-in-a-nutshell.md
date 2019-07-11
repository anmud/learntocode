# Gatsby DataLayer in a Nutshell

- Sincse `Gatby` is created on top of `React` we know our `projects` will consist of `components`. 
- In some of these components or mayby in all of them we would want to display `data`. That could be all kinds of `data` => (API's, Headless CMS, JSON, Markdown, SiteMetadata). 
- In order to get that `data` we will utilize `qraphql` - a syntax that describes how to ask for the `data`. It allows us to spesify what `data` we would need and uses the `type system` to describe that `data`.  
- in `gatsby` we can test our `qhaphql queries` in `GraphiQL IDE`;
- and once we are ready to render our `data` we can do that using `<StaticQuery>` or `<PageQuery>`.
`<StaticQuery>` can be used in any `component` including `pages`. But `<PageQuery>` we can use only in the `page` components. What makes `<PageQuery>` more flexible - is the simple fact that we can pass `variables` into `<PageQuery>`. 