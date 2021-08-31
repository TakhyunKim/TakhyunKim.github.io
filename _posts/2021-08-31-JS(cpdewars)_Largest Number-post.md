---
title: "codewars - Largest Number"
data: 2021-08-31 15:01:30 -0400
categories: Javascript
---

Given a list of non-negative integers nums, arrange them such that they form the largest number.

Note: The result may be very large, so you need to return a string instead of an integer.

Examples
```
Example 1:

Input: nums = [10,2]
Output: "210"
Example 2:

Input: nums = [3,30,34,5,9]
Output: "9534330"
Example 3:

Input: nums = [1]
Output: "1"
Example 4:

Input: nums = [10]
Output: "10"
```

code
---
```js
const largestNumber = function(nums) {
  if (!nums || !nums.length) {
      return '0';
  }

  nums.sort((a, b) => `${b}${a}` - `${a}${b}`);

  if(nums[0] === 0) {
      return '0';
  }


  return nums.join('');
};
```

소요 시간
---
1시간

다른 사람의 코드
---
```js
var largestNumber = function(nums) {
nums = nums.sort(compare)
  if (parseInt(nums) === 0) {
      return '0';
  } else {
      return nums.toString().split(",").join("")
  }
}
function compare(a,b){
  var ab = a.toString() + b.toString();
  var ba = b.toString() + a.toString();
  return ba - ab;
};
```
