---
title: "codewars - Replace With Alphabet Position"
date: 2020-01-02 15:16:30 -0400
categories: Javascript
---

Welcome.<br>

In this kata you are required to, given a string, replace every letter with its position in the alphabet.<br>

If anything in the text isn't a letter, ignore it and don't return it.<br>

"a" = 1, "b" = 2, etc.<br>

code
---
```js
function alphabetPosition(text) {
  let newArr = text.toUpperCase().split(" ").join("").split("");
  let result = "";
  
  for (let i = 0; i < newArr.length; i++) {
    if (newArr[i].charCodeAt(0) >= 65 && newArr[i].charCodeAt(0) <= 90) {
      result += newArr[i].charCodeAt(0) - 64 + " ";
    }
  }
  return result.substr(0, result.length - 1);
}
```

풀이 시간 & 막힌 부분
---
40분

- 막힌 점은 딱히 없었다. 처음에는 알파벳을 배열로 해서 index로 접근하려고 하였으나<br>
  좀 더 좋은 방법이 없을까하면서 생각한 결과 아스키 코드를 활용하게 되었다.<br>
  이 점까지 접근하는데 있어서 시간이 좀 걸렸다.<br>
