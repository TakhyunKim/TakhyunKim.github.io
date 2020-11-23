---
title: "codewars - Your order, please"
date: 2020-11-23 21:35:30 -0400
categories: Javascript
---

Your task is to sort a given string. Each word in the string will contain a single number. <br>

This number is the position the word should have in the result.<br>

Note: Numbers can be from 1 to 9. So 1 will be the first word (not 0).<br>

If the input string is empty, return an empty string. The words in the input String will only contain valid consecutive numbers.<br>

```js
"is2 Thi1s T4est 3a"  -->  "Thi1s is2 3a T4est"
"4of Fo1r pe6ople g3ood th5e the2"  -->  "Fo1r the2 g3ood 4of th5e pe6ople"
""  -->  ""
```

code
---
```js
function order(words){
  // ...
  const testArr = words.split(" ");
  const newArr = [];
  const result = [];
  
  if (words.length === 0) {
    return "";
  }
   
  for (let i = 0; i < testArr.length; i++) {
    for (let j = 0; j < testArr[i].length; j++) {
      if (!isNaN(testArr[i][j])) {
        const obj = {};
        
        obj["test"] = [testArr[i], +testArr[i][j]];
        newArr.push(obj); 
      }
    }
  }

  newArr.sort(function(a, b) {
    return a["test"][1] - b["test"][1];
  });
  
//   console.log(newArr);
  for (let i = 0; i < newArr.length; i++) {
    result.push(newArr[i]["test"][0]);
  }
  
  return result.join(" ");
}
```

실수 사항 및 놓친 사항
---
형변환과 같은 디테일한 부분을 많이 놓쳤다.<br>
알고리즘 내용이 길어져서 실수한 사항도 많다. 

소요시간
---
45분
