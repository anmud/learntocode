# Converting links to buttons with CSS

Now what we gonna do is taking "learn more" `links` inside of our `promos` and style them so that they look more like `buttons`. We need to add some inline style to the `anchor tags` of the links (text-shadow: 0px - X offset 2px- on the Y offset 2px at blur ).


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
						<td valign="top" class="logo" bgcolor="#ffffff" style="padding: 10px 20px 0px 30px; border-left: 1px solid #dbc064; border-right: 1px solid #dbc064; border-top: 1px solid #dbc064;"> 
                            <a href="#"><img style="margin-left: 15px"  src="images/logo_large.gif" alt="Our Vineyard" width="585" heigh="45" border="0"></a> 
						</td>
					</tr>
					<tr><!--headline row-->
						<td valign="top" class="headline" bgcolor="#ffffff"  
							style="padding: 15px 20px 5px 30px; border-left: 1px solid #dbc064; border-right: 1px solid #dbc064; font-family: Arial, Helvetica, sans-serif; font-size: 16px; line-height: 22px;">
                              <h1 style="margin: 0px 0px 15px 0px; font-weigt: normal; font-size: 32px; color: #723c7f;">Main Heading Here</h1>
                        </td>
                        </tr>
                        <tr><!--banner row-->
                            <td valign="top" bgcolor="#f5f2e5" class="banner" 
                        style="border-left: 1px solid #dbc064; border-right: 1px solid #dbc064;">
                           <img src="images/banner_large.jpg" width="638" height="180" alt="Photo of Our Vineyard">
                            </td>
                        </tr>
					<tr><!--content row-->
                        <td valign="top" bgcolor="#f5f2e5" class="content" style="padding: 30px 30px 10px 30px;  
						border-right: 1px solid #dbc064; 
						border-left: 1px solid #dbc064; 
						font-family:Arial, Helvetica, sans-serif; font-size: 16px; 
                        line-height:22px; color: #654308;  
                        background: #f5f2e5 url(images/banner_large_ghost.jpg) no repeat 0px 0px"> 
                              Lorem ipsum dolor sit amet consec tetur adip isicing elit sed do eiusmod tempor 
							  incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam quis 
							   nostrud exercita tion ullamco laboris nisi ut aliquip ex ea commodo consequat.  
							   Duis aute irure dolor in reprehenderit in voluptate velit esse cillum eu fugiat nulla.
							 <br><br>
							 Enjoy,
							 <br>
							 <img src="images/chris.gif" alt="Chris" width="90" height="40">
							 
                        </td>
                    </tr>
                    <tr><!--promos row-->
                        <td valign="top" bgcolor="#f5f2e5" class="promos" style="padding: 10px 30px 25px 30px;  
						border-right:1px solid #dbc064; border-left:1px solid #dbc064;  
                        background-color: #f5f2e5; font-family: Arial, Helvetica, sans-serif;">
                        <table class="promo_1" width="270" align="left"><!--create a table-->
                             <tr>
								 <td>
									 <img class="promo" alt="Promo image 1" src="images/promo_1_large.jpg">
                                      <h3 style="font-size:16px;">Promo heading here</h3>
                                      Lorem ipsum dolor sit amet consectetur incididunt ut labore et dolore magna aliqua elit sed do eiusmod.
                                       <br><br>
                                       <a href="#" style="background-color: #71a412; border-radius: 5px; color: #fff; padding: 5px 10px 5px 10px;  
									text-decoration: none; text-shadow: 0px 2px 2px #3a5606">Learn more</a><!--style links to buttons-->
     
								 </td>
							 </tr>
                           </table>
                           <table class="promo_2" width="270" align="right">
							<tr>
								<td>
								   <img class="promo" alt="Promo image 2" src="images/promo_2_large.jpg">
								   <h3 style="font-size:16px;">Promo heading here</h3>
								   Lorem ipsum dolor sit amet consectetur incididunt ut labore et dolore magna aliqua elit sed do eiusmod.
								   <br><br>
								   <a href="#">Learn more</a>
								   
								</td>
                            </tr>
                            <tr><!--callouts row-->
                                <td valign="top" bgcolor="#55315d" class="callout" style="background-color: #55315d; 
						 padding: 30px; border-right: 1px solid #dbc064;  
                        border-bottom: 1px solid #dbc064; border-left: 1px solid #dbc064;">
                                <table class="callout_1" width="135" align="left" border="0" cellspacing="0" cellpadding="0"><!--callout 1-->
	                                <tr>
		                               <td valign="top" width="135" style="padding-left: 10px; padding-right: 10px; font-family:Arial, Helvetica, sans-serif; font-size:13px; line-height: 16px; color: #ffffff;">
			                              <img src="images/icon_grapes.gif" width="75" height="75"><br>
		                                    	Lorem ipsum dolor sit amet conctetur adipi eiu smod incid amet idun.
			                              <br><br>
			                           <a href="#">Learn more</a>
		                               </td>
                                	</tr>
                                      </table>
                                      <table class="callout_2" width="135" align="left" border="0" cellspacing="0" cellpadding="0"><!--callout 2-->
	<tr>
		<td valign="top" width="135" style="padding-left: 10px; padding-right: 10px; font-family:Arial, Helvetica, sans-serif; font-size:13px; line-height: 16px; color: #ffffff;">
			<img src="images/icon_bottle.gif" width="75" height="75"><br>
			Ddolore eu fugiat nulla pariatur cupi datat excepteur occaet cupi noin.
			<br><br>
			<a href="#">Learn more</a>
		</td>
	</tr>
</table>

<table class="callout_3" width="135" align="left" border="0" cellspacing="0" cellpadding="0"><!--callout 3-->
	<tr>
		<td valign="top" width="135" style="padding-left: 10px; padding-right: 10px; font-family: Arial, Helvetica, sans-serif; font-size: 13px; line-height: 16px; color: #ffffff;">
			<img src="images/icon_basket.gif" width="75" height="75"><br>
			Eiusmod tempor inci didunt ut magna aliqua ut enim ad iam quis.
			<br><br>
			<a href="#">Learn more</a>
		</td>
	</tr>
</table>

<table class="callout_4" width="135" align="left" border="0" cellspacing="0" cellpadding="0"><!--callout 4-->
	<tr>
		<td valign="top" width="135" style="padding-left: 10px; padding-right: 10px; font-family: Arial, Helvetica, sans-serif; font-size: 13px; line-height: 16px; color: #ffffff;">
			<img src="images/icon_camera.gif" width="75" height="75"><br>
			Excepteur sint occaecat cupidatat non proident sunt in culpa qui molit.
			<br><br>
			<a href="#">Learn more</a>
		</td>
	</tr>
</table>
               <br style="clear: both;">

        </td>
 </tr><!--end callouts row-->
						  
            <tr><!--footer row-->
                <td valign="top" class="footer" style="padding: 10px 0px 30px 0px; font-family: Arial, Helvetica, sans-serif; font-size: 11px; color: #b2a16e;">
                   &copy; Your Company Name. PLEASE DO NOT REPLY TO THIS MESSAGE:
                   <br><br>
                   Your <a href="#" style="color:#000000;">privacy</a> is important to us. Please use this link to <a href="#" style="color:#000000;">unsubscribe</a>.
                  <br><br>
                  Lorem ipsum dolor sit amet consectetur adipi sicing elit sed do eiusmod tempor inci didunt ut labore et dolore iqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.

                </td>
             </tr>
				</table>
         </td>
         </tr>
	 </table>
	</body>	
</html>
```
![button-style](../button-style.png)

Some `email clients` will not be able to render the `body radius`, so instead of the round-corner buttons we will have square buttons; and in other cases some `email clients` can't render the background color. 

