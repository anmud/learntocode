# Module Pattern

In `JavaScript`, the word `“modules”` refers to small units of independent, reusable code. They are the foundation of many JavaScript design patterns and are critically necessary when building any non-trivial JavaScript-based application. Most JavaScript `modules` export an `object` literal, a `function`, or a `constructor`. `Modules` that export a `string` containing an `HTML template` or a `CSS stylesheet` are also common.
We can store both `public` and `private` `methods` and `variables` inside a single `object`. That allows us to create a `public facing API` for the `methods` that we want to expose to the world, while still encapsulating private `variables` and `methods` in a `closure scope`.  

### Example

```js
var Car = function(){

  var gasolineLevel = 10; 

  function useGas(amt){      
    if(gasolineLevel - amt < 0){ 
      console.log("out of gas :[");
    } else { 
      gasolineLevel -= amt; 
    }
  };

  return {
    radioStation: "104.5",

    changeStation: function(station){   
      this.radioStation = station;
    },
    go: function(speed){ useGas(speed); }  
  };
};
var ferrari = Car();
ferrari.go(2); //undefined 
ferrari.go(10); // "out of gas :["
```

Because our private `properties` are not returned they are not available outside of out `module`.

Using the `return` statement we can `return` an `object literal` that `reveals` only the `methods` or `properties` we want to be publicly available.



