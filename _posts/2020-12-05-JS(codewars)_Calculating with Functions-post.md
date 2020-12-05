---
title: "codewars -Calculating with Functions"
date: 2020-12-05 14:36:30 -0400
categories: Javascript
---

This time we want to write calculations using functions and get the results.<br>
Let's have a look at some examples:<br>
```
seven(times(five())); // must return 35
four(plus(nine())); // must return 13
eight(minus(three())); // must return 5
six(dividedBy(two())); // must return 3
```
Requirements:

There must be a function for each number from 0 ("zero") to 9 ("nine")<br>
There must be a function for each of the following mathematical operations:<br>
plus, minus, times, dividedBy (divided_by in Ruby and Python)<br>
Each calculation consist of exactly one operation and two numbers<br>
The most outer function represents the left operand, the most inner function represents the right operand<br>
Division should be integer division. For example, this should return 2, not 2.666666...:<br>
eight(dividedBy(three()));<br>

code
---
```js
function expression(Num, calFunc) {
  if (!calFunc) {
    return Num
  }
  
  return calFunc(Num);
}

function zero(func) {
  return expression(0, func);
}
function one(func) {
  return expression(1, func);
}
function two(func) {
  return expression(2, func);
}
function three(func) {
  return expression(3, func);
}
function four(func) {
  return expression(4, func);
}
function five(func) {
  return expression(5, func);
}
function six(func) {
  return expression(6, func);
}
function seven(func) {
  return expression(7, func);
}
function eight(func) {
  return expression(8, func);
}
function nine(func) {
  return expression(9, func);
}

function plus(x) {
  return function (y) {
    return y + x;
  }
}
function minus(x) {
  return function (y) {
    return y - x;
  }
}
function times(x) {
  return function (y) {
    return y * x;
  }
}
function dividedBy(x) {
  return function (y) {
    return Math.floor(y / x);
  }
}
```

풀이 방식
---
underdash에서 쓰였던 고차함수 방식에서 착안한 해결방법이었습니다.<br>
베이스로 쓰일 expression 함수를 만들어 첫번째 인자로 num, 두번째 인자로 함수를<br>
받아 이 후 숫자 함수에서 전부 적용하였습니다.<br>

연산 함수에서는 그 뜻에 맞는 연산을 하게끔 진행하였습니다.<br>
(크게 어려웠던 문제는 아니었다.)<br>

풀면서 문제되었던 점
---
큰 문제는 아니었고, 최종 제출 테스트 코드 중 나눗셈 부분에서<br>
결과값이 반올림이 되었어야 한다는 점 때문에 Math.floor 메서드를 활용하여<br>
해결하였다.<br>

풀이 시간
---
30분

다른 사람 풀이
---
```js
['zero', 'one', 'two', 'three', 'four', 'five', 'six', 'seven', 'eight', 'nine']
.forEach(function (name, n) {
  this[name] = function (f) { return f ? f(n) : n }
});

function plus(n)      { return function (a) { return a + n } }
function minus(n)     { return function (a) { return a - n } }
function times(n)     { return function (a) { return a * n } }
function dividedBy(n) { return function (a) { return a / n } }
```

위 풀이법이 되게 인상 깊었다.<br>
숫자를 전부 배열화하여 forEach를 통해 순회, 그리고 바로 적용까지 한다는 점에서<br>
너무너무 인상 깊은 코드였다.<br>
그 외에 또 색다른 코드들은 하기 링크를 통해 확인해보자!<br>
https://www.codewars.com/kata/525f3eda17c7cd9f9e000b39/solutions/javascript
