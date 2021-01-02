---
title: "codewars - Find the smallest integer in the array"
date: 2021-01-02 16:04:30 -0400
categories: Javascript
---

Given an array of integers your solution should find the smallest integer.<br>

For example:<br>

Given [34, 15, 88, 2] your solution will return 2<br>
Given [34, -345, -1, 100] your solution will return -345<br>
You can assume, for the purpose of this kata, that the supplied array will not be empty.<br>

code
---
```js
class SmallestIntegerFinder {
  findSmallestInt(args) {
    const argsSortArr = args.sort((a, b) => {return a - b});
    
    return argsSortArr[0];
  }
}
```

풀이 과정 및 소요 시간
---
1분
