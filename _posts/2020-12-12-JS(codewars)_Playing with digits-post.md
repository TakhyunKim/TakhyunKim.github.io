---
title: "codewars - Playing with digits"
date: 2020-12-12 21:57:30 -0400
categories: Javascript
---

Some numbers have funny properties. For example:

```
89 --> 8¹ + 9² = 89 * 1

695 --> 6² + 9³ + 5⁴= 1390 = 695 * 2

46288 --> 4³ + 6⁴+ 2⁵ + 8⁶ + 8⁷ = 2360688 = 46288 * 51

Given a positive integer n written as abcd... (a, b, c, d... being digits) and a positive integer p

we want to find a positive integer k, if it exists, such as the sum of the digits of n taken to the successive powers of p is equal to k * n.
In other words:

Is there an integer k such as : (a ^ p + b ^ (p+1) + c ^(p+2) + d ^ (p+3) + ...) = n * k

If it is the case we will return k, if not return -1.
```

Note: n and p will always be given as strictly positive integers.

code
---
```js
function digPow(n, p){
  // ...
  const newArr = n.toString().split("");
  const newArr2 = [];
  let powNum = p;
  
  for (let i = 0; i < newArr.length; i++) {
    newArr2.push(Math.pow(newArr[i], powNum));
    powNum++;
  }
  
  const sumNum = newArr2.reduce(function(prev, next) {
    return prev + next;
  });
  
  if (Number.isInteger(sumNum / n)) {
    return sumNum / n;
  } else {
    return -1;
  }
}
```

풀이 과정
---
거듭 제곱 연산자 pow를 활용한다는 걸 베이스로 깔고 시작했습니다.<br>
이 후 정수 판별로 최종 결과값 분기점을 구성하면 될 것이다라는 생각을 가지고 로직을 구성하였습니다.<br>
위 두 가지 생각을 가지고 문제를 풀었다는 것이 결과를 도출하는데 있어 큰 역할을 했다고 생각합니다.<br>

소요 시간
---
30분

다른 풀이법
---
```js
function dogPow(n, p) {
  var x = String(n).split("").reduce((s, d, i) => s + Math.pow(d, p + i), 0);
  
  return x % n ? -1 : x / n;
}
``` 

신기하다..
