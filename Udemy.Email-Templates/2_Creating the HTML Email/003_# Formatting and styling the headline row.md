# Formatting and styling the headline row

First let's add some styling to the `<td>` and then inside add `h1` tag. I this `<td>` tag we have the `font size` and the `font family` setup; so, if we specify a oartucular inlibe styles in this `<td>` every setup text inside will get these properties, unless we wrap them inside of another `object`. So, the `h1` in our case is the separate `object` for this `<td>`. So, we gonna add a new inline style to the `h1` so we can style it separately. 
Any time we have a specific block inside of a `<td>` we have to add font sizes and other different properties. To look our `logo` nicely let's get back to `logo` and add some `margin` to the logo image. That's gonna have the `logo` a little bit to the left, so it aligns with `heading`. 
### HTML
```html
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
	<head>
		<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
		<title>Our Vineyard</title>
		<style type="text/css">
			/* css goes here */
		</style>
	</head>	
	<body bgcolor="#efe1b0">    
	<table width="100%" border="0" cellsapcing="0" cellpadding="0" bgcolor="#efe1b0">
   
		 <tr>
         <td>
            <table class="container" width="640" align="center" border="0" cellpaddong="0" cellspasing="0"> <!--main email container with 7 rows inside-->
					<tr><!--logo row-->
						<td valign="top" class="logo" bgcolor="#ffffff" style="padding: 10px 20px 0px 30px; border-left: 1px solid #dbc064; border-right: 1px solid #dbc064; border-top: 1px solid #dbc064;"> <!--add style-->
                            <a href="#"><img style="margin-left: 15px"  src="images/logo_large.gif" alt="Our Vineyard" width="585" heigh="45" border="0"></a> <!--add image, add margin to logo-->
						</td>
					</tr>
					<tr><!--headline row-->
						<td valign="top" class="headline" bgcolor="#ffffff"  
							style="padding: 15px 20px 5px 30px; border-left: 1px solid #dbc064; border-right: 1px solid #dbc064; font-family: Arial, Helvetica, sans-serif; font-size: 16px; line-height: 22px;">
                              <h1 style="margin: 0px 0px 15px 0px; font-weigt: normal; font-size: 32px; color: #723c7f;">Main Heading Here</h1><!--add style to the heading-->
						</td>
					
				</table>
         </td>
         </tr>
	 </table>
	</body>	
</html>
```
![heading-part](../heading-part.png)

