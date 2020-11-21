---
title: "codewars - spinWords"
date: 2020-11-22 01:07:30 -0400
categories: Javascript
---

spinWords
---
하나 이상의 단어 문자열을 받아 통일한 문자열을 반환, 만약 해당 문자열의 길이가<br>
5 이상일 경우 단어를 모두 뒤집어서 반환.<br>

code
---
```js

function spinWords(something){
  //TODO Have fun :)
  const cloneArgumentArr = something.split(" ");
  const result = [];
  
  for (let i = 0; i < cloneArgumentArr.length; i++) {
    if (cloneArgumentArr[i].length > 4) {
      let newStr = cloneArgumentArr[i].split("").reverse().join("");
    
      result.push(newStr);
    } else {
      result.push(cloneArgumentArr[i]);
    }
  }
  
  return result.join(" ");
}
```

놓친 사항 / 실수 사항
---
split, join 사용 미숙

소요시간
---
20분
