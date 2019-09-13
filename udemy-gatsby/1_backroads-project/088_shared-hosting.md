# Shared Hosting

Let's say you prefer shared hosting. Let's do it for our project **but** 
> note! we'll do just with gatsy specific information.

you can use `inmotion hosting`, `godaddy`, or any other options.
we need to setup our production build (gatsby build) - but we need also make our `environment variables` available -  the easiest way to do that is - to create in the root the file named `".env.production"`, set there `sape id` and `access tocken` => then go to `git.ignore` file and type  the `.env.production` there as well => run `gatsby build`. 

Now we can go to our `fpt client` we use(you can choose any); => grab all the content from the `public` folder of our project and drag and drop it in the `ftp client`. 

