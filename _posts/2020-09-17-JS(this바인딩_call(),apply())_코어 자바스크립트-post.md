---
title: "명시적으로 this를 바인딩하는 방법"
date: 2020-09-17 16:02:28 -0400
categories: Javascript
---
명시적으로 this를 바인딩하는 방법
===
this에 별도의 대상을 바인딩하는 방법 2가지에 대해 작성하였습니다.

call 메서드
---

``` javascript
Function.prototype.call(thisArg[,arg1[,arg2[,...]]])
```
위와 같은 형태를 띄고 있으며 메서드의 호출 주체인 함수를 즉시 실행하도록 하는 메서드입니다.
이 때 call 메서드의 첫 번째 인자를 this로 바인딩하고, 이 후의 인자들을 호출할 함수의 매개변수로 합니다.
함수를 그냥 실행하면 this는 전역객체를 참조하지만, call 메서드를 이용하면 임의의 객체를 this로 지정가능합니다.
``` javascript
var func = function (a, b, c) {
  console.log(this, a, b, c);
};

func(1, 2, 3); // widow{...} 1 2 3
func.call({x: 1}, 4, 5, 6); // {x:1}, 4, 5, 6
```
메서드에 대해서도 마찬가지로 객체의 메서드를 그냥 호출하면 this는 객체를 참조하지만
call 메서드를 이용하면 임의의 객체를 this로 지정할 수 있습니다.
``` javascript 
var obj = {
  a: 1,
  method: function (x, y) {
    console.log(this.a, x, y);
  }
};

obj.method(2, 3);
obj.method.call({a: 4}, 5, 6); // 4 5 6 
```

apply 메서드
---

``` javascript
Function.prototype.apply(thisArg[, argsArray])
```
apply 메서드는 call 메서드와 기능적으로 완전히 동일합니다. call 메서드는 첫 번째
인자를 제외한 나머지 모든 인자들을 호출할 함수의 매개변수로 지정하는 반면, apply 메서드는
두 번째 인자를 배열로 받아 그 배열의 요소들을 호출할 함수의 매개변수로 지정한다는 점에서만
차이가 있습니다.

``` javascript
var func = function (a, b, c){
  console.log(this, a, b, c);
};
func.apply({x: 1}, [4, 5, 6]); // {x: 1} 4 5 6

var obj = {
  a: 1,
  method: function (x, y) {
    console.log(this.a, x, y);
  }
};
obj.method.apply({a: 4}, [5, 6]); // 4 5 6 
```
