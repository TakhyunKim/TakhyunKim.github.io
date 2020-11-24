---
title: "codewars - Your order, please"
date: 2020-11-23 21:35:30 -0400
categories: Javascript
---

Implement the function unique_in_order which takes as argument a sequence and <br>
returns a list of items without any elements with the same value next to each other and <br>
preserving the original order of elements.<br>


For example:
```js
uniqueInOrder('AAAABBBCCDAABBB') == ['A', 'B', 'C', 'D', 'A', 'B']
uniqueInOrder('ABBCcAD')         == ['A', 'B', 'C', 'c', 'A', 'D']
uniqueInOrder([1,2,2,3,3])       == [1,2,3]
```

code
---
```js
var uniqueInOrder=function(iterable){
  //your code here - remember iterable can be a string or an array
  
  const result = [];
  
  let str;
  
  for (let i = 0; i < iterable.length; i++) {
    if (iterable[i] !== str) {
      result.push(str = iterable[i]);
    }
  }
  
  return result;
}
```

소요 시간
---
30분
