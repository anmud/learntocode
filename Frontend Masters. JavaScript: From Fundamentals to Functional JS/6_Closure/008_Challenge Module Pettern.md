# Module Pattern Challenge

1. Using the `module pattern`, design a toaster. Use your creativity here and think about what you want your users to be able to access on the outside of your toaster vs what you don't want them to be able to touch.

```js
var Toaster = function(){
    //some private methods and properties
    
    return {
      //some public methods and properties, etc
    };
};
```
### Solution

```js
var Toaster = function(){
var maxTemp = 500; 
var temp = 0,
return{
  setTemp : function(newTemp){
      if (newTemp > maxTemp){
          console.log("That temp is too high!")
      }else {
          temp = newTemp;
      }
  }
};
};
var myToaster = Toaster();
myToaster.setTemp(200); 
```

