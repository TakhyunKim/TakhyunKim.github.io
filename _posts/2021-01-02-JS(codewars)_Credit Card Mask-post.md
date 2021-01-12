---
title: "codewars - Credit Card Mask?"
date: 2021-01-12 16:28:30 -0400
categories: Javascript
---

Usually when you buy something, you're asked whether your credit card number, <br>
phone number or answer to your most secret question is still correct. <br>
However, since someone could look over your shoulder, you don't want that shown on your screen. <br>
Instead, we mask it.<br>

Your task is to write a function maskify, which changes all but the last four characters into '#'.<br>

Examples
```
maskify("4556364607935616") == "############5616"
maskify(     "64607935616") ==      "#######5616"
maskify(               "1") ==                "1"
maskify(                "") ==                 ""

// "What was the name of your first pet?"
maskify("Skippy")                                   == "##ippy"
maskify("Nananananananananananananananana Batman!") == "####################################man!"
````

code
---
```js
// return masked string
function maskify(cc) {
  console.log(cc.length);
  if (cc.length > 4) {
    return `${"#".repeat(cc.length - 4)}${cc.slice(-4)}`;
  }

  return cc;
}

```

소요 시간
---
10분

다른 사람의 코드
---
```js
function maskify(cc) {
  return cc.slice(0, -4).replace(/./g, '#') + cc.slice(-4);
}
```
