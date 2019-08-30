# Single Tour Query

When writing the `query` for the single tour we also need to get the `date`, but the response is actually not very friendly. 

![date-query](./date-query.png)

If we look at the docs in `Prisma playground` and find our `field`, namely "start" - and then we can see that we can in fact pass the `argumenets`, and one of them is very useful - `formatString`. Gatsby in fact behind the scenes is using the `Moment.js` and if we pass `formatString` as an `argument`, we can format our start date as we want. 

![date-query-argument](./date-query-argument.png)

Next, we need to get the `description` and it was the long-text format in the Contentful content-model, so in the query it should be actually an `object` - `description{description}`.

![description-query](./description-query.png)

Next - the journey - it is a JSON format. To be specific with the journey - we'll add two subfields - day and info (we have them in the content-model)

![journey-query](./journey-query.png)

Lats thing - images. 

![images-query](./images-query.png)