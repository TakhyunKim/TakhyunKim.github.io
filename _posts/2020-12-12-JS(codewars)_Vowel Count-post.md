---
title: "codewars - Vowel Count"
date: 2020-12-12 21:54:30 -0400
categories: Javascript
---

Return the number (count) of vowels in the given string.<br>

We will consider a, e, i, o, u as vowels for this Kata (but not y).<br>

The input string will only consist of lower case letters and/or spaces.<br>

code
---
```js
function getCount(str) {
  var vowelsCount = 0;
  
  // enter your majic here
  
  for (let j = 0; j < str.length; j++) {
    if (str[j] === "a") {
      vowelsCount++;
    }
    if (str[j] === "e") {
      vowelsCount++;
    }  
    if (str[j] === "i") {
      vowelsCount++;
    }   
    if (str[j] === "o") {
      vowelsCount++;
    }   
    if (str[j] === "u") {
      vowelsCount++;
    }     
  }
  
  return vowelsCount;
}
```

문제 풀이 및 문제점
---
a,e,i,o,u가 포함되어 있는 경우 카운팅하여 최종값을 출력<br>
출제자의 의도를 이해하지 못하고 헤맸음..<br>
국어 능력이 떨어지는 모양 ;<br>

소요시간
---
30분
