# Drag and Drop

To continue working on the project we need the account on [Netlify](https://app.netlify.com) - a platform for automating web projects.

As we are working with Netlify we have two options:
- we can use the continuous deployment using Github 
- or we have 'dag-and-drop' option

What we would want is run `gatsby build` command where we will have our production project: where all the static `html` will be created as well as minified `js` and `css`. 

In order to do that in the terminal we write `gatsby build`, and now within the `public` folder (our production application lives here) we gonna get all the needed files. 

Now we can drag and drop this `public folder` to Netlify. If we wanna change the name of the site we can head over to the site settings and change the name there. Then we can just use the link of the site - and we have our application online!!!

There are downfalls of this lind of setting:
Let's imagine the scenario when we wanna change something on our site, that already has been deployed, we can surely make changes, but then first need to stop the `dev server`, then again run `gatsby build` and again go to our project on Netlify and drag and drop new public file. So, we need to do this after every change we wanna make on the site. 

The better way is to use `continuos deployment`. 