# For Loops Challenge

### INSTRUCTIONS

1. Write a `for` loop to build a string of numbers from `0` to `4`, separated by spaces, and store the string in the variable `text`.

```js
for(let i = 0; i <= 4; i += 1) {
  text += i + ' ';
}
print(text); //Should print `0 1 2 3 4 `.
```

2. Write a `for` loop to build a string of numbers from `1` to `5`, separated by spaces, and store the string in the variable `text`.

```js
for(let num = 1; num <=5; num += 1){
  text += num + ' ';
}
print(text); //Should print `1 2 3 4 5 `.
```

3. Write a `for` loop to build a string of numbers from `5` to `1`, separated by spaces, and store the string in the variable `text`.

```js
for( let num = 5; num >= 1; num -= 1){
  text += num + ' ';
}

print(text); //Should print `5 4 3 2 1 `.
```

4. Write a `for` loop to build a string of numbers from `5` to `50--by 5's`. The numbers should be separated by spaces, and stored in the variable `text`.

```js
for(let num = 5; num <=50; num +=5){
  text += num + ' ';
}

print(text); //Should print `5 10 15 20 25 30 35 40 45 50 `.
```

5. Write a `for` loop to build a string of numbers from `50` to `5--by 5's`. The numbers should be separated by spaces, and stored in the variable `text`.

```js
for(let num = 50; num >=5; num -=5){
  text += num + ' ';
}

print(text); //Should print `50 45 40 35 30 25 20 15 10 5 `.
```


