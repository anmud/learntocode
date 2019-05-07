# HTTP Protocol . Promise

## HTTP Protocol

#### What is a server and a client?

- A `server` is a computer that listens for `responses`
- A `client` is a computer that calls the `server`

#### How do `server` and `client` communicate?
They communicate via a `http protocol`: `protocol` is a `language` for communication between computers. The main important thing about a `protocol`, it has `strict rules` for communication.

What are the `rules` for communicaiton between `computers` via `http`?

**Request:** is done by the `client`

- url: http://www.firebasedatabase.com/?30435345
- method: GET, POST, PUT, DETELE
- header: Accept: application/json, Authorization: APIKEY345345, Content-Type: application/json 
- body: {"id": 1, "name": Anastasia"}

note 1.  Accept: application/json - I accept `data` only in `JSON format`
note 2. Authorization: APIKEY345345 - the `key` wich gives the opportunity to request for the `data` in case of authorisation
note 3. Content-Type: application/json - I send you `data` in `JSON form`

**Response:** is done by the `server`

- header: Access-Control-Allow-Origin: * [read more here](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)
- status: 200 (ok), 400 (error) [read more here](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status)
- body: {"id": 1, "name": "Anastasia"}

note 1. Access-Control-Allow-Origin: * - you can use all `data bases`

Wildcard `*`.


#### What is a JSON and why do we communicate with JSON?

**JSON** - JavaScript Object Notation.

1. **JSON encode:** translate `data` from `in-memory` to `JSON format`

```js
JSON.stringify({id: 1, name: "Anastasia"}) // encoded version: {"id": 1, "name": "Anastasia"}
```

2. **JSON decode:** translate `data` from `JSON fromat` to `in-memory`

```js
JSON.parse({"id": 1, "name": "Anastasia"}) // decodes to {id: 1, name: "Anastasia"}

// In memory representation
const body = {
  id: 1,
  name: "Anastasia"
}
```

## Promise

How to make a `request` to a server? Here in the example we use `fetch` library, http protocol and a promise(`.then function`)

```js
const callMe = response => response.json()
const callMeNext = encodedJson => console.log(encodedJson)

fetch('https://jsonplaceholder.typicode.com/todos/1', {
  method: "GET",
  headers: {
  "Accept": "application/json"
  }
})
.then(callMe)
.then(callMeNext)
.catch(error => console.log(error))

// console.log: {userId: 1, id: 1, title: "delectus aut autem", completed: false}
```

##### Another syntax is to use `async-await`

```js
const todo = async () => {
  const todo = await fetch('https://jsonplaceholder.typicode.com/todos/1', {
  										method: "GET",
  										headers: {
  										"Accept": "application/json"
  										}
						})
  const encodedTodo = await todo.json()
  const todoShow = encodedTodo
  console.log(todoShow)
  return todoShow 
}

todo()

// {userId: 1, id: 1, title: "delectus aut autem", completed: false}
```

`.then()` works like a `map function`. When the `data` from a `response` comes, this `data` goes to `.then()` function (promise) as a `parameter`. 

```js
const resp = [{userId: 1, id: 1, title: "delectus aut autem", completed: false}]

const test = resp
				.map(x => x)
				.map(x => ({...x, title: x.title.toUpperCase()}))
				.map(x => ({...x, id: 2}))

console.log(test)
// [{…}]
// 0: {userId: 1, id: 2, title: "DELECTUS AUT AUTEM", completed: false}

```
























