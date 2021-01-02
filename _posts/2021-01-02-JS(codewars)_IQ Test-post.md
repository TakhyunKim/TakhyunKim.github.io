---
title: "codewars - IQ Test"
date: 2021-01-02 15:56:30 -0400
categories: Javascript
---

Bob is preparing to pass IQ test. The most frequent task in this test is to find out which <br>
one of the given numbers differs from the others. <br>
Bob observed that one number usually differs from the others in evenness. <br>
Help Bob — to check his answers, he needs a program that among the given numbers <br>
finds one that is different in evenness, and return a position of this number.<br>

! Keep in mind that your task is to help Bob solve a real IQ test, which means indexes of the elements start from 1 (not 0)<br>

##Examples :
```
iqTest("2 4 7 8 10") => 3 // Third number is odd, while the rest of the numbers are even

iqTest("1 2 1 1") => 2 // Second number is even, while the rest of the numbers are odd
```

code
---
```js
function iqTest(numbers){
  // ...
  const newArr = numbers.split(" ").map(val => val * 1);
  
  let evenArr = newArr.filter(val => val % 2 === 0);
  
  let obbArr = newArr.filter(val => val % 2 === 1);

  return evenArr.length > obbArr.length ?
    newArr.indexOf(obbArr[0]) + 1 :
    newArr.indexOf(evenArr[0]) + 1;
}
```

풀이 과정 및 소요시간
---
풀이 과정은 단순했다.<br>
우선 짝수와 홀수에 대한 값을 나누기 위해 매개변수 numbers를 배열화하였고,<br>
이 후 짝수 배열과 홀수 배열을 나눠 체크하였다.<br>

return에서는 삼항 연산자를 통해 해결하였다.<br>

소요시간은 30분 정도 소요<br>
