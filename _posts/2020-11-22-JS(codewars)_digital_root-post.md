---
title: "codewars - digital_root"
date: 2020-11-22 11:22:30 -0400
categories: Javascript
---

digital_root
---
Digital root is the recursive sum of all the digits in a number.<br>

Given n, take the sum of the digits of n. If that value has more than one digit,<br>
continue reducing in this way until a single-digit number is produced. <br>
The input will be a non-negative integer.<br>

숫자의 각 자릿수를 더한 값을 리턴하는 함수를 작성하시오.<br>
만약 더한 값이 두 자릿수 이상일 경우 한 자릿수가 될 때까지 연산해야 합니다.<br>

code
---
```js
function digital_root(n) {
  let sum = 0;
  const argStr = n.toString().split("");
  
  for (let i = 0; i < argStr.length; i++) {
    sum += parseInt(argStr[i]);
  }
  
  let test = sum.toString().split("");

  
  if (test.length > 1) {
    return digital_root(sum);
  } else if (test.length === 1) {
    return sum;
  }
}
```

풀이 과정 중 실수 사항 & 놓친 사항
---
실수라기 보다는 초반 코드 방향성은 옳게 잡았는데 split 메소드를 활용하여<br>
배열에 쪼개서 만드는 방법이 있는데도, 처음에는 for문을 활용하여 코드의 양을<br>
많이 작성한 점이 개선 사항 중 하나였고, 이는 바로 적용하였습니다.<br>

두 번째로는 하단의 test라는 배열에 length가 1 이상 즉, 자릿수가 10의 자릿수 이상일 경우<br>
재귀 함수와 같이 활용하여 재 연산을 하도록 하였는데,<br>
이 과정에서 return을 붙이지 않아 재 연산을 했을 경우 undefined가 출력되는 결과를 초래했다.<br>

상당히 기초적인 문제지만, 놓쳐서는 안될 부분이었고 분명히 개선해야할 점이라고 생각된다.<br>

소요 시간
---
40분
