# Continuous Deployment

When we have our project we can create the `new repo` if it was not created earlier. The wto commant we;ll be interested in: 
- setting up the remote url 
- pushing it to that remote url

So in the terminal of the project we can write: 
- git init to create a new repository
- git add . (use point if you wanna add all the files)
- then git commit -m "some message"
- git push -u origin master

Once we do that, we have our project on the Github. 

Now we can go to the Netlify and create a new site from Git - just push the button "new site from Git", choose github, then `build` command will gonna run for us,  push "deploy". So, every changes that we gonna commit/push for the github project will automatically update the site. 