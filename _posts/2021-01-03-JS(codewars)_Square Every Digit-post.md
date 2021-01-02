---
title: "codewars -Square Every Digit"
date: 2021-01-03 01:36:30 -0400
categories: Javascript
---

Welcome. In this kata, you are asked to square every digit of a number and concatenate them.<br>

For example, if we run 9119 through the function, 811181 will come out, because 92 is 81 and 12 is 1.<br>

Note: The function accepts an integer and returns an integer<br>

code
---
```js
function squareDigits(num){
  const newStr = num.toString();
  let resultArr = [];
  
  for (let i = 0; i < newStr.length; i++) {
    resultArr.push(Math.pow(newStr[i], 2));
  }
  
  return +resultArr.join("");
}
```

소요 시간
---
10분

풀이 과정
---
pow를 활용하여 각 자릿수에 대하여 제곱하여 배열에 push하였고<br>
return 할 시 문자열을 숫자열로 형변환 후 join을 통해 값을 합쳤다.<br>

다른 사람 풀이
---
```js
function squareDigits(num){
  return Number(('' + num).split('').map(function (val) { return val * val;}).join(''));
  
}
```
