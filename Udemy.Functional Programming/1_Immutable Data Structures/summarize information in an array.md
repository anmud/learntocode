# Summarize information in an array

Let's say we have the following `array` with the students' garades: 

```js
const grades = [60, 55, 80, 90, 99, 92, 75, 72]
```
1. First we wanna know the average grade
2. Second how many A's, B's, C's, D's...students are

We wanna solve this challenge in an immutable way. the tool to use in this case is the `reduce()` function. Reduce() expects a `transformation function` as a `parameter`. 

Lets' solve our first task. We'll do it in two steps: first we add all `grades` together and get the `total`. Then we'll figure out how many grades there are in the array (the count). And find the average by dividing the total number to the count. 

```js
const grades = [60, 55, 80, 90, 99, 92, 75, 72]
const total = grades.reduce(sum);

function sum(acc, grade){
    return acc + grade
}

const count = grades.length;

console.log(total/count) //77.875
```
For the second part of our challenge we'll use `reduce()` function. 

```js
const grades = [60, 55, 80, 90, 99, 92, 75, 72]
const total = grades.reduce(sum);

function sum(acc, grade){
    return acc + grade
}

const count = grades.length;
const letterGradeCount = grades.reduce(groupByGrade, {})

function groupByGrade(acc, grade){
    const {a =0, b=0, c=0, d=0, f=0} = acc
if (grade>=90){
    return {...acc, a: a + 1 };
}else if (grade >= 80){
    return {...acc, b: b+1}
}else if (grade >= 70){
    return {...acc, c: c+1}
}else if (grade >= 60){
    return {...acc, d: d+1}
}else {
    return {...acc, f: f+1}
}
}

console.log(letterGradeCount) //{a: 3, b: 1, c: 2, d: 1, f: 1}

```

### Exersise

```js
const reviews = [4.5, 4.0, 5.0, 2.0, 1.0, 5.0, 3.0, 4.0, 1.0, 5.0, 4.5, 3.0, 2.5, 2.0];

// 1. Using the reduce function, create an object that
// has properties for each review value, where the value
// of the property is the number of reviews with that score.
// for example, the answer should be shaped like this:
// { 4.5: 1, 4.0: 2 ...}

const countGroupedByReview = reviews.reduce(groupBy, {});

function groupBy (acc, review){
  const count = acc[review] || 0;
  return {...acc, [review]: count + 1}
}

console.log(countGroupedByReview); // {1:2, 2:2, 2.5:1, 3:2, 4:2, 4.5:2, 5:3 }
```