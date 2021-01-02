---
title: "codewars - Highest and Lowest"
date: 2021-01-03 00:57:30 -0400
categories: Javascript
---

In this little assignment you are given a string of space separated numbers, <br>
and have to return the highest and lowest number.<br>

Example:<br>
```
highAndLow("1 2 3 4 5");  // return "5 1"
highAndLow("1 2 -3 4 5"); // return "5 -3"
highAndLow("1 9 3 4 -5"); // return "9 -5"
```
Notes:<br>

All numbers are valid Int32, no need to validate them.<br>
There will always be at least one number in the input string.<br>
Output string must be two numbers separated by a single space, and highest number is first.<br>

code
---
```js
function highAndLow(numbers){
  const numbersArr = numbers.split(" ").map(val => val * 1);
  
  const minVal = Math.min(...numbersArr);
  const maxVal = Math.max(...numbersArr);
  
  let result = `${maxVal} ${minVal}`;
  
  return result;
}
```

풀이 과정 및 소요 시간
---
소요 시간 : 10분<br>

가장 작은 값, 큰 값을 구하는 문제이므로 min과 max를 활용하면 된다고 생각하였고<br>
매개 변수를 배열화하였고 이 후 템플릿 리터럴을 활용해서 return 하였다.<br>
