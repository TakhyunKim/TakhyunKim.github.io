---
title: "codewars - Sum of two lowest positive integers"
date: 2021-01-03 01:19:30 -0400
categories: Javascript
---

Create a function that returns the sum of the two lowest positive numbers <br>
given an array of minimum 4 positive integers. No floats or non-positive integers will be passed.<br>

For example, when an array is passed like [19, 5, 42, 2, 77], the output should be 7.<br>

[10, 343445353, 3453445, 3453545353453] should return 3453455.<br>

code
---
```js
function sumTwoSmallestNumbers(numbers) {  
  const newArr = numbers.sort((a, b) => {return a - b});
  
  return +`${newArr[0] + newArr[1]}`;
}
```

소요 시간
---
15분

풀이 과정
---
sort로 오름차순 정렬을 통해서 첫번째, 두번째 인덱스를 더했으며 <br>
더하는 과정은 변수 선언으로 따로 계산하기 보다 템플릿 리터럴을 활용하여 문제를 해결하였다.<br>
