---
title: "codewars - Counting sheep..."
date: 2021-01-05 20:40:30 -0400
categories: Javascript
---


Consider an array/list of sheep where some sheep may be missing from their place. <br>
We need a function that counts the number of sheep present in the array (true means present).<br>

For example,
```js
[true,  true,  true,  false,
  true,  true,  true,  true ,
  true,  false, true,  false,
  true,  false, false, true ,
  true,  true,  true,  true ,
  false, false, true,  true]
```
The correct answer would be 17.<br>

Hint: Don't forget to check for bad values like null/undefined<br>

code
---
```js
function countSheeps(arrayOfSheep) {
  // TODO May the force be with you
  
  let count = 0;
  
  for (let i = 0; i < arrayOfSheep.length; i++) {
    if (arrayOfSheep[i] === true) {
      count++
    }
  }
  
  return count;
}
```

풀이 시간
---
1분

다른 사람 풀이
---
```js
function countSheeps(arrayOfSheeps) {
  return arrayOfSheeps.filter(Boolean).length;
}
```
