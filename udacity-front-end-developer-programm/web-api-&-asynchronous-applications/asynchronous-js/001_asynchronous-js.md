# Asynchronous JavaScript

JavaScript is a single threaded programming language, which means for the most part it will be run as a single process in your computer (essentially writing and running it top to bottom).

To be an effective web developer you have to be comfortable writing async code when the situation calls for it. For those times JavaScript does have a few async tricks up its sleeve. One of the most common is `setTimeout()` which allows you to break out of the inherent JS behavior of executing code line by line starting at the top.

## Async Promises

While there have always been some async work arounds in JS, including `setTimeout()`, and `AJAX`, more recently a tool called `Promises` has been introduced natively to JavaScript, and `Promises` are now the accepted *best practice* for writing asynchronous functions in JavaScript.

You can think of `Promises` as a special function that either satisfy (resolve) or fail (reject) to execute a task, and then executes the corresponding actions, usually another task with the returned data in the case of 'resolved' and usually throw an error in the case of 'reject'.

Here is the basic anatomy of a Promise:

```js
var promise = new Promise(function(resolve, reject) {
  // do a thing, possibly async, then…

  if (/* everything turned out fine */) {
    resolve("Stuff worked!");
  }
  else {
    reject(Error("It broke"));
  }
});
```

There are many methods to handle asynchronous work already, however Promises are the recommended option because they give you flexibility, intuitive syntax, and easy error handling. Promises are an amazing development in JavaScript, but until ES2017 (ES8) they still required extra boilerplate code, called generators, to run asynchronously. Now however, with the addition of native `async` functions to JavaScript, we can *easily apply the async keywords to a Promise to execute asynchronous JavaScript code*.

To make a `fetch()` call, or any other methods inside of a function, asynchronous we must *use the keywords provided by JavaScript*. Here is an example of what it would look like to turn the `fetch function` from the previous example into an asynchronous function:

```js
const postData = async ( url = '', data = {})=>{
    // console.log(data)
      const response = await fetch(url, {
      method: 'POST', // *GET, POST, PUT, DELETE, etc.
      credentials: 'same-origin', // include, *same-origin, omit
      headers: {
          'Content-Type': 'application/json',
      },
      body: JSON.stringify(data), // body data type must match "Content-Type" header        
    });

      try {
        const newData = await response.json();
        console.log(newData);
        return newData
      }catch(error) {
      console.log("error", error);
      // appropriately handle the error
      }
  }

  postData('/addMovie', {movie:' the matrix', score: 5})
```

`postData` is an `async arrow function` that is called with parameters on the last line of code. It is asynchronous because of the keyword `async` placed before its parameters. Once you mark a function as 'async' you have access to the keywords `await`, `try`, and `catch` which mirror the underlying Promise functionality of resolving or rejecting a condition-- here the condition is successfully making a POST request to the specified route. The `await` keyword is used in places where the next actions requires data from the current action so we want to tell our program to wait until the data has been received before continuing with the next steps-- this is the magic of ASYNC JavaScript.

In the next lesson we will learn how to pair JavaScript async fetch functions with Web APIS to unleash the dynamic power of front-end programming.

More on Async JS
For a more detailed overview on Promises and why they matter, read the article [here](https://developers.google.com/web/fundamentals/primers/promises).

## Asynchronous JavaScript with Fetch. Introduction

The `Fetch API` is build on top of native `JS promises`, which make it ideal for working with WEb APIs. 

A **Web API** - is an application programming interface for either a web server or a Web Browser. Some of the popular web APIs are weather data and financial data. But really, Web API can be anywhere that someone has organized information and made that data available to query through an API. 

## Credentials and API keys

When working with a Web API, there is a little bit of setup you have to do even before you start coding. 

1. The first step is that for most WEb APIs, you'll have to *sign up* for `developer credentials`. This is very easy to do if you go to any website. They usually have a `Developer Tab` or something you can click on and it's free. You put your email address and you'll get a `key` which is a code as a `string of characters`, and that is what you'll use to access the Web API. 

2. The second part is that you actually gonna build a `query` by making a `URL` that includes the `key` that you got. 

Many APIs require you to `sign up`, `create credentials`, and use an `API key` in order to start sending requests to the API.

## Adding Fetch to Your Code

Use the `base URL` that's provided to you by the `Web API documentation`. What this neabs is when people go in their browser, to this URL, if they completed it by adding `"animal"` at the end, like "tiger", then **that would query the "tiger" part of the Web API.** 

1. So, the first step in making a web API is actually to *set variables to hold the base URL* and *your API key*.  
2. And then we surely need to know what animal to add. 
3. For that we gonna use `the DOM selector` so that we can take in the `dynamic value` that a user enters. 

Here is the `client side code` that would make a `GET` request to the `animal info API`:

```js
let baseURL = 'http://api.animalinfo.org/data/?animal='
let apiKey = '&appid=9f15e45060...';

document.getElementById('generate').addEventListener('click', performAction);

function performAction(e){
const newAnimal =  document.getElementById('animal').value;
getAnimal(baseURL,newAnimal, apiKey)

}
const getAnimal = async (baseURL, animal, key)=>{

  const res = await fetch(baseURL+animal+key)
  try {

    const data = await res.json();
    console.log(data)
    return data;
  }  catch(error) {
    console.log("error", error);
    // appropriately handle the error
  }
}
```

---

**TASK:** 

Write an async function to make a `GET` request that has one argument: a `url` to make the GET request to.

**SOLUTION:**

```js
const retrieveData = async (url='') =>{ 
  const request = await fetch(url);
  try {
  // Transform into JSON
  const allData = await request.json()
  }
  catch(error) {
    console.log("error", error);
    // appropriately handle the error
  }
}
```

---

## Async Fetch with Web APIs Demo

```js
let baseURL = 'http://api.animalinfo.org/data/?animal='
let apiKey = '&appid=9f15e45060...';

document.getElementById('generate').addEventListener('click', performAction);

function performAction(e){
const newAnimal =  document.getElementById('animal').value; //let's say the value is "tiger"
getAnimal(baseURL,newAnimal, apiKey)
}

const getAnimal = async (baseURL, animal, key)=>{

  const res = await fetch(baseURL+animal+key)
  try {

    const data = await res.json();
    console.log(data)
    return data;
  }  catch(error) {
    console.log("error", error);
    // appropriately handle the error
  }
}
```

So, we've setup the parts to our URL and then, we've added a simple `event listener` called "click", and within the callback function `performAction` we wanna call `getAnimal`. The `getAnimal` function is an asynchronous function that take three parameters, which are: the base URL, the animal we wanna get and the API key. Then we rebuild our URL into a `fetch call`, so actually the URL we have now looks like `http://api.animalinfo.org/data/?animal=tiger&appid=9f15e45060`. Snd that is will let us query a Web API. 

Let's look at this if it'll be a little bit tricky. We are going to fetch an API endpoint that we've setup called "Fake Animal Data". 

```js
let baseURL = 'http://api.animalinfo.org/data/?animal='
let apiKey = '&appid=9f15e45060...';

document.getElementById('generate').addEventListener('click', performAction);

function performAction(e){
const newAnimal =  document.getElementById('animal').value; //let's say the value is "tiger"
getAnimal(baseURL,newAnimal, apiKey)
}

const getAnimal = async (baseURL, animal, key)=>{

  const res = await fetch('fakeAnimalData')
  try {

    const data = await res.json();
    console.log(data)
    return data;
  }  catch(error) {
    console.log("error", error);
    // appropriately handle the error
  }
}
```

In our `server.js` file we have our dummy API endpoint data

**server.js**
```js

//dummy API endpoint
const fakeData = {
  animal: 'lion',
  fact: 'lions are fun'
}

app.get('/fakeAnimalData', getFakeData) // a GET route

function getFakeData(req,res){
  res.send(fakeData)
}

const animalData = [];

app.get('/all', getData)

function getData(req, res){
  res.send(animalData)
  console.log(animalData)
}
```

And we gonna send back to our `API request` an animal -  "lion" and a fact - "lions are fun'. This `object` actually simulates what you're likely het back from a real `API call`. 

Then we have a `GET route` setup, that says "get fake animal data" and a callback function just sends back out fake data. This does simulate how it would work with an API. So, that is an example of how we can make a` GET request` using `fetch to a Web API`.

Let's go deeper. So, when we are calling the `getAnimal` function: 
- the first thing we make it an `asynchronous` function by adding the `async` keyword before the function itself. This gives us access to the async keywords as `await`, `try` and `catch`. 
- once we are into the meat of our function, we set a `variable` to hold our `fetch calls return`. The `await` keyword is what makes this all work, because `await` is telling the script *not to go on to the next part untill it's recieved the data that it needs*, cos our `fetch call` is callling to our Web API. 
- once we've setup what our condition is (namely, wait for the return), then we'll do a `try` and  a `catch`. A `try` is what happens if everything goes well. So, assuming evrything is going well and we got our `data` back, we wanna get this `new data` that is in `JSON` format. 
- `catch` stands for the situations that if smth. goes wrong we have some idea of it. 

> The **JavaScript Fetch API** provides a more elegant interface and syntax for working with `HTTP requests`. This makes it a perfect fit for working with `Web API data`. Up next, we will learn how to chain `Fetch calls` together to dynamically update the `UI` of an app.

- [Fetch over view on MDN](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)
- [Using Fetch on MDN](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch)

## Chaining Promises - Dependent GET and POST Requests

So, let's think for a second about aour animal Web API app example. Imagine we also wanna to add a `feature` to our `app` where users can enter their favourite thing about their favourite animal. And then we wanna be able to save all the information which is: the info we get back from the API (the name of the animal and a fact about it), and from the users their favourite thing about animal - we wanna take all that and save it to our `app` so that we can use it later. 

We would need two `fetch calls` - first a `GET request` to the animal Web API,  and then we would need to make a `POST request` to store all the `data` we received *locally* in our `app`. `Async promises` are perfect for this kind of thing.

Because the `Fetch API` is build on top of promises, we can use the syntax `.then()` to chain `actions` with `fetch calls`.

Inside `.then()` we could call another `async` function to make a `POST` request to store this `data` in our app. Assuming a `POST route` has been setup on the *server side* to add `data` it received to the `app endpoint`, we could simply **call** the function we have been using to create `POST` requests on the *client side* and pass it the `POST route url` and the `data` we want to save to our app. The only tricky part (which can also be fun!), is that we need to use the `returned data`, and data that we retrieve from a `DOM element` to create the *structure* for our `POST request`.

As a reminder, the `postData()` function takes a `URL`, and a `data object` as parameters. To build the `data object` using `data` received from the previous `fetch call` we can use **dot notation**. So we could set our first elements like this:

```js
postData('/addAnimal', {animal:data.animal, fact: data.fact} )
```

But we also want to include the *users favorite thing about the animal*, which we can add using the `variable name` which selects the `textarea` where the users response is. So our final code for creating a `POST route` to save the `data` to our app would look like this:

```js
postData('/addAnimal', {animal:data.animal, fact: data.fact, fav:favFact} )
```

Then **on the server side** to actually add the sent data to our app, we would use this code:
We've created a `post route`, and we call this from the client side `postData( '/addAnimal', {animal.data.animal, fact: data.fact, fav: favFact} )`, we gonna create a `new entry` in our `data endpoint`, using the `request.body` thah comes back to us.
Then we're going to push all that in the `new entry` into `animal data` and acting as our `API endpoint` from which we can gather data and do what we want. 

```js
const animalData = [];

// GET route
app.get('/all', getData)

function getData(req, res){
  res.send(animalData)
  console.log(animalData)
}

//POST route
app.post('/addAnimal', addAnimal);

function addAnimal(req,res){

  newEntry = {
    animal: req.body.animal,
    facts: req.body.fact,
    fav: req.body.fav
  }

  animalData.push(newEntry)
  console.log(animalData)
}
```

**client side**

```js
function performAction(e){
  const fav = document.getElementById('fav').value;
  
getAnimal('/fakeAnimalData')
.then(function(data){
  console.log(data)
  // add data to POST request
  postData( '/addAnimal', {animal.data.animal, fact: data.fact, fav: favFact} );
});
}; 

const getAnimal = async (url) => {
  const res = await fetch(url);
  try{
    const data = await res.json();
    console.log(data)
    return data;
  }
  catch(error){
    console.log('error', error)
  }
}

const postData = async (url = '', data = {}) => {
  const response = await fetch(url,{
    method: 'POST',
    credentials: 'same-orogin',
    headers: {
      'Content-Type' : 'application/json',
    },
    body: JSON.stringify(data),
  });

  try{
    const newData = await reaponse.json();
    console.log(newData);
    return newData
  }
  catch(error){
    console.log(error)
  }
}

```

## Dynamic UI Updates

One of the most useful applications of `chain promises` is to use `Web API data` to dynamically update the `UI of an app`. 

> Dynamically updating the UI of an app means *creating or changing DOM elements based on data recieved in real time from the app or from an API*

Three steps to dynamically updating a UI

- create a `selector` for the `element` you want to update. This would be an HTML element using `id` or `class`
- identify the `data` that you wanna to update that `element` with
- approprietly set that `data` to that `element`

Here is what it would look like to use chained GET and POST requests to retrieve information from our animal Web API, and then update DOM elements accordingly:

**HTML**

```html
<label for="animal">Enter the name of your favorite animal</label>
<input id="animal" name="animal">
<textarea id="favorite" placeholder="Enter your favorite thing about your favorite animal" rows="9" cols="50"></textarea>
<button id = "generate">GO</button>
```

**JS**

```js
document.getElementById('generate').addEventListener('click', performAction);

function performAction(e){
  const newAnimal =  document.getElementById('animal').value;
  const favFact =  document.getElementById('favorite').value;

  getAnimal('/animalData',)
  // New Syntax!
  .then(function(data){
    // Add data
    console.log(data);
    postData('/addAnimal', {animal:data.animal, fact: data.fact, fav:favFact} );
  })
  .then(
    updateUI()
  )
}

const updateUI = async () => {
  const request = await fetch('/all');
  try{
    const allData = await request.json();
    document.getElementById('animalName').innerHTML = allData[0].animal;
    document.getElementById('animalFact').innerHTML = allData[0].facts;
    document.getElementById('animalFav').innerHTML = allData[0].fav;

  }catch(error){
    console.log("error", error);
  }
}
```

Notice how calling the function to update the UI is the last thing we do -- this is because the update `UI` function depends on data from each of the other functions, so each `Promise` must be resolved successfully before we can update the `UI`. This demonstrates why `native Promises` and the `Fetch API` are such powerful tools for Asynchronous JavaScript.

---

**EXERCISE:**

1) In the file `getPost.js`, write a function that chains together the two `async functions` you have previously written, so that you make a `POST` request to the `/animal` route, and then retrieve the data with a `GET request` to the `/all` path.

You should pass in a `data object` of your favorite animal as the second argument for the `POST request`.

Call your function as the last line of code in the file named `getPost.js`.

**SOLUTION:**

*getPOst.js*

```js
// Async POST
const postData = async ( url = '', data = {})=>{

    const response = await fetch(url, {
    method: 'POST', 
    credentials: 'same-origin', 
    headers: {
        'Content-Type': 'application/json',
    },
    body: JSON.stringify(data), // body data type must match "Content-Type" header        
  });

    try {
      const newData = await response.json();
      return newData;
    }catch(error) {
    console.log("error", error);
    }
};

// Async GET
const retrieveData = async (url='') =>{ 
  const request = await fetch(url);
  try {
  // Transform into JSON
  const allData = await request.json()
  }
  catch(error) {
    console.log("error", error);
    // appropriately handle the error
  }
};

// TODO-Chain your async functions to post an animal then GET the resulting data

const nameAnimal = (url,animal) => {
    postData('/animal', {fav: 'cat'})
    .then(function(data){
        retrieveData('/all')
    })
}

// TODO-Call the chained function
nameAnimal()
```

*server.js*

```js
/* Empty JS object to act as endpoint for all routes */
projectData = {};

/* Express to run server and routes */
const express = require('express');

/* Start up an instance of app */
const app = express();

/* Dependencies */
const bodyParser = require('body-parser')
/* Middleware*/
app.use(bodyParser.urlencoded({ extended: false }));
app.use(bodyParser.json());
const cors = require('cors');
app.use(cors());

/* Initialize the main project folder*/
app.use(express.static('website'));

const port = 3000;
/* Spin up the server*/
const server = app.listen(port, listening);
 function listening(){
    // console.log(server);
    console.log(`running on localhost: ${port}`);
  };

// GET route
app.get('/all', sendData);

function sendData (request, response) {
  response.send(projectData);
};

// POST route
app.post('/add', callBack);

function callBack(req,res){
  res.send('POST received');
};

// POST an animal
const data = [];

app.post('/animal', addAnimal);

function addAnimal (req,res){
    data.push(req.body);
};

```

---

EXERCISE: 

Assume you have a `div` with the `id`: `score`. Assume you also have the `data object` below returned from a `fetch()` call-- what line of code would you write to assign the `innerHTML` property of `<div id=”score”></div>` to the `value` of the key `returnedScore`.

```js
data = {
  name: ‘who cares’,
  returnedScore: 6
}
```

SOLUTION:

```js
document.getElementById('score').innerHTML = data.returnedScore;
```

---





