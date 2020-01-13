# Responsive Layout

## A simlpe Blog Page

**index.html**

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <title>Demo 1</title>
    <meta
      content="width=device-width, initial-scale=1, maximum-scale=1"
      name="viewport"
    />
    <link rel="stylesheet" href="style.css">

  </head>

  <body>
  <div class = "container">
    <div class="header box">Header</div>
    <div class="sidebar box">
      <h1>Blog Posts</h1>
      <!-- Add Link To Blog Here -->
      <a href="post.html">Most Resent Posts</a>
    </div>
    <div class="content box">Content
    
    </div>
    <div class="footer box">Footer</div>
  </div>
  </body>
</html>
```

**style.css**

```css
body{
    background-color: #444;
}
.container{
    /* Step 1: Set display to grid */
      display:grid;
      width: 90%;
      margin: auto;
      margin-top: 150px;
   /* Step 2: setup rows and columns */
      /* grid-template-columns: repeat(3, 1fr); */
      grid-template-columns: 30px repeat(7, 1fr);
      grid-template-rows: 70px 400px 1fr;
      grid-template-areas: 
      "hd hd hd hd hd hd hd hd"
      "sd sd main main main main main main"
      "ft ft ft ft ft ft ft ft";
      /* border: 2px solid yellow;*/

  }
  .box{
  /* width: 250px;
    height: 150px; */
    border: 1px solid red;
    background: #F8FA9D;
    }

  .header{
    /* row start/column start/ row end/ column end */
    grid-area:hd;
  }

  .footer{
    grid-area: ft;  
  }
  .sidebar{
    grid-area: sd;
  }
  .content{
    grid-area: main;
  }
```

**post.html**

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <title>Exercise 1</title>
    <meta
      content="width=device-width, initial-scale=1, maximum-scale=1"
      name="viewport"
    />
    <link rel="stylesheet" href="blog.css">
  </head>
  <body>
  <div class = "container">
    <div class="header box">Header</div>
    <div class="feature"></div>
    <div class="content box">Content</div>
    <div class="footer box">Footer
    <a href="index.html">Click here to go back home</a>
    </div>
  </div>
  </body>
</html>
```
**blog.css**

```css
.container{
      display:grid;
      grid-template-rows: 100px 350px 600px 100px; 
      grid-template-areas: 
      "hd hd hd hd hd hd hd hd"
      "feat feat feat feat feat feat feat feat"
      "main main main main main main main main"
      "ft ft ft ft ft ft ft ft";
      border: 2px solid yellow;

  }
  .box{
    border: 1px solid red;
    background: #F8FA9D;
    }

  .header{
    grid-area: "hd";
  }    

  .footer{
       grid-area: "ft";
  }
      
 .feature{
     grid-area: "feat";
  }
  .content{
     grid-area: "main";
     background-image: url("images/waterfall.jpeg");
     background-size: contain;
     background-repeat: no-repeat;
  }
```


CSS Grid can be used to setup multiple displays within a single site. I

Separate pages within a web app can be stored in the same folder and linked to each other using <a> tags to create links with the name of the file as the target. For example, in a file index.html you could use the following code to link to another file in the same directory named go.html:

```html
<a href="go.html">Go to page</a>
```

**Further Research**

For more on Grid Layouts, see the below articles.

(Creating complex Grid layouts)[https://rachelandrew.co.uk/archives/2015/02/04/css-grid-layout-creating-complex-grids/]
(Nesting & overlapping of Grid items)[https://gridbyexample.com/examples/example21/]

