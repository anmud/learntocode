# Formatting and styling the logo row

Let's add some `attributes` to the `logo <td>`: `valign`,  `class`, `bgcolor` ... Inside the `<td>` let's add an `image` which will be the large logo. We'll set the `width` and `height`; also we wanna make sure that the `logo` is clickable to our website, so let's add an `anchor` tag. 

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
					<tr>
						<td valign="top" class="logo" bgcolor="#ffffff" style="padding: 10px 20px 0px 30px; border-left: 1px solid #dbc064; border-right: 1px solid #dbc064; border-top: 1px solid #dbc064;"> <!--add style-->
                            <a href="#"><img src="images/logo_large.gif" alt="Our Vineyard" width="585" heigh="45" border="0"></a> <!--add image-->
						</td>
					</tr>
					<tr>
						<td>

						</td>
					</tr>
					<tr>
						<td>

						</td>
					</tr>
					<tr>
						<td>

						</td>
					</tr>
					<tr>
						<td>

						</td>
					</tr>
					<tr>
						<td>

						</td>
					</tr>
					<tr>
						<td>

						</td>
					</tr>
				</table>
         </td>
         </tr>
	 </table>
	</body>	
</html>
```
![logo-part](../logo-part.png)
