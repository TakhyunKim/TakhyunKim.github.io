---
title: "codewars - Which are in?"
date: 2021-01-05 20:59:30 -0400
categories: Javascript
---


Given two arrays of strings a1 and a2 return a sorted array r in <br>
lexicographical order of the strings of a1 which are substrings of strings of a2.<br>
```
#Example 1: a1 = ["arp", "live", "strong"]

a2 = ["lively", "alive", "harp", "sharp", "armstrong"]

returns ["arp", "live", "strong"]

#Example 2: a1 = ["tarp", "mice", "bull"]

a2 = ["lively", "alive", "harp", "sharp", "armstrong"]

returns []
```
Notes:
Arrays are written in "general" notation. See "Your Test Cases" for examples in your language.<br>

In Shell bash a1 and a2 are strings. The return is a string where words are separated by commas.<br>

Beware: r must be without duplicates.
Don't mutate the inputs.

code
---
```js
function inArray(array1,array2){
  const newArr = array2.join(" ");
  
  return array1.filter(value => newArr.indexOf(value) !== -1 && value !== undefined).sort();
}
```

소요 시간
---
20분

다른 사람 풀이
---
```js
function inArray(array1,array2){
  return array1
    .filter(a1 => array2.find(a2 => a2.match(a1)))
    .sort()
}
```
