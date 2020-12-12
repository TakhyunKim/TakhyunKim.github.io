---
title: "codewars - Duplicate Encoder"
date: 2020-12-12 16:24:30 -0400
categories: Javascript
---

The goal of this exercise is to convert a string to a new string where each character <br>
in the new string is "(" if that character appears only once in the original string, or ")" <br>
if that character appears more than once in the original string. <br>
Ignore capitalization when determining if a character is a duplicate.<br>

Examples
```
"din"      =>  "((("
"recede"   =>  "()()()"
"Success"  =>  ")())())"
"(( @"     =>  "))(("
```

code
---
```js
function duplicateEncode(word){
    // ...
  const newWord = word.toUpperCase();
  const countObj = {};
  const result = [];
  
  for (let i = 0; i < newWord.length; i++) {
    if (countObj.hasOwnProperty(newWord[i])) {
      countObj[newWord[i]]++;
    } else {
      countObj[newWord[i]] = 1;
    }
  }
  console.log(countObj);
  for (let i = 0; i < newWord.length; i++) {
    if (countObj[newWord[i]] > 1) {
      result.push(")");
    } else {
      result.push("(");      
    }
  }
  
  return result.join("");
}
```

풀이 과정
---
객체로 카운팅하여, 초기값은 1 이 후 중복된 문자열이 있을 경우<br>
증감 연산자를 통해 값을 변경하여 중복된 값 여부를 확인<br>
객체의 value를 통해 최종 결과 배열에 값을 push해서 결과값을 출력<br>

풀이 과정에서 문제되었던 것
---
자꾸 객체의 값이 1로 통일되거나, 2로 값이 통일되었는데<br>
if else문으로 분기점을 확실히 구분했어야 하는데 이를 구분하지 않고<br>
`countObj[newWord[i]] = 1;` <= 이 구문을 for문 돌 때마다 실행되어<br>
값이 자꾸 초기화되는 버그를 만들었음ㅠㅡㅠ<br>

다른 풀이법
---
```js
function duplicateEncode(word){
  return word
    .toLowerCase()
    .split('')
    .map( function (a, i, w) {
      return w.indexOf(a) == w.lastIndexOf(a) ? '(' : ')'
    })
    .join('');
}
```

......ㅋㅋㅋ.....ㅋㅋㅋㅋ 신박하누... 
