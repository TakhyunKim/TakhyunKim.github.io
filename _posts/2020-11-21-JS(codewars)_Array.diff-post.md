---
title: "codewars - Array.diff"
date: 2020-11-21 00:22:30 -0400
categories: Javascript
---

Array.diff
---
Your goal in this kata is to implement a difference function, <br>
which subtracts one list from another and returns the result.<br>
It should remove all values from list a, which are present in list b.<br>

위 과제 목표는 다른 목록에서 한 목록을 빼고 결과를 반환하는 차이 함수를 구현하는 것입니다.<br>
배열 b에 있는 값을 배열 a에서 모두 제거해야 합니다.<br>

예시 1)
``` js
arrayDiff([1,2],[1]) == [2]
```

예시 2)
```js
arrayDiff([1,2,2,2,3],[2]) == [1,3]
```


code 
---
```js
function arrayDiff(a, b) {
  const copyArgumentZero = a.slice();
  const arr = [];
  const result = [];
  const container = {};
  
  for (let i = 0; i < arguments[0].length; i++) {
    container[arguments[0][i]] = 1;   
  }
  
  for (let i = 0; i < arguments[1].length; i++) {
    if (container.hasOwnProperty(arguments[1][i])) {
      container[arguments[1][i]]++;
    }
  }
  
  for (const prop in container) {
    if (container[prop] === 1) {
      arr.push(+prop);
    } 
  }
  
  for (let i = 0; i < copyArgumentZero.length; i++) {
    for (let j = 0; j < arr.length; j++) {
      if (copyArgumentZero[i] === arr[j]) {
        result.push(copyArgumentZero[i]);
      }
    }
  }
  
  return result; 
}
```

코드 작성 시 실수한 점 혹은 놓친 점
---

**1. 방식 접근에서의 문제**<br>
맨 처음 접근했을 때, 첫 번째 문제점은 만약 첫 번째 배열이 [1,2,2,2,3]와 같이<br>
중복되는 숫자가 있을 경우 이 중복되는 숫자를 어떻게 처리하냐는 점이었습니다.<br>

간단하게 코드를 작성하자면<br>
``` js
var arr = [1,2,2,2,3];
var obj = {};

for (var i = 0; i < arr.length; i++) {
  obj[arr[i]] = 1;
}

console.log(obj); // {1:1, 2:1, 3:1}
```
위 예제와 같은 결과가 나옵니다. 방식 자체는 각 값마다 value를 1로 잡아 <br>
이 후 두 번째 인자에 값과 동일한 경우 해당 value를 1씩 증가시켜,<br>
value가 1인 경우에만 값을 살리는 방식으로 접근하였는데,<br>
결국 이 경우에는 중복되는 값은 찾을 수 없다라는 문제가 있었습니다.<br>

이 후 현재 위 방식으로 걸러내야 할 값을 찾고, 이 obj를 토대로<br>
값을 찾는 방식으로 해결하였습니다.<br>

**2. 중첩 for문 사용 시 변수 혼용해서 사용**<br>
이는 일단 단순 실수이며, 스스로 반성해야하고 개선해야할 사항 중에 하나입니다.<br>
특히 for문을 중첩하여 사용할 경우 많이 발생되는 실수이며,<br>
``` js
  for (let i = 0; i < copyArgumentZero.length; i++) {
    for (let j = 0; i < arr.length; i++) {
```

두 번째 for문에서 j를 i로 적어서 에러를 발생시켰습니다.<br>

**3. 숫자열, 문자열**<br>
```js
  for (const prop in container) {
    if (container[prop] === 1) {
      arr.push(+prop);
    } 
  }
```
위 코드에서 +prop이 보이는데 기본적으로 for in문에서 저 prop은 사용 시<br>
문자열로 변경이 되어있는 상태입니다. 이는 자바스크립트가 자동으로 변경하는 부분으로<br>
type coercion이라는 개념을 통해 알아보는게 좋을 것 같습니다.<br>

결국 문자열로 값을 받아오고 이를 이 후에 문자열을 기준으로 비교하게 되는데,<br>
이 과정에서 숫자열과 문자열을 비교해서 원하는 결과를 얻어내지 못하게 됩니다.<br>
실제로 이 문제 때문에 약 20분 정도 시간이 소요되었습니다.<br>
debugger를 통해 문제점을 찾았고, 해결한 뒤 테스트를 해본 결과<br>
테스트 케이스 45개를 모두 통과하였습니다.<br>

소요시간
---
40분

문제 출처
---
codewar - javascript 부문 && 2020 11 21 토요일
