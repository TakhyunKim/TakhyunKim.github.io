---
title: "codewars - Split Strings"
date: 2021-01-03 21:02:30 -0400
categories: Javascript
---

Complete the solution so that it splits the string into pairs of two characters.<br>
If the string contains an odd number of characters then it should replace <br>
the missing second character of the final pair with an underscore ('_').<br>

Examples:
```
solution('abc') // should return ['ab', 'c_']
solution('abcdef') // should return ['ab', 'cd', 'ef']
```
code
---
```js
function solution(str) {
  let result = [];
  
  while(str.length > 1) {
    result.push(str.slice(0, 2));
    str = str.slice(2, str.length);
  }
  
  if (str.length !== 0) {
    result.push(str + "_");
  }
  
  return result;
}
```

소요시간
---
20분

다른 사람 풀이법
---
```js
function solution(str){
  arr = [];
  for(var i = 0; i < str.length; i += 2){
    second = str[i+1] || '_';
    arr.push(str[i] + second);
  }
  return arr;
}

```

