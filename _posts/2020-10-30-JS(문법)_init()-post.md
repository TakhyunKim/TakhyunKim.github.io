---
title: "자바스크립트의 init함수"
date: 2020-10-30 01:46:28 -0400
categories: Javascript
---

자바스크립트의 init함수
---
기본적으로 자바스크립트에서는 init이라는 내장 함수는 존재하지 않습니다.<br>
해당 함수는 사용자가 임의로(의도적으로) 이름을 붙여서 사용하는 것입니다.<br>
init은 보통 초기화의 의미를 지닌 함수나 객체를 사용할 경우에 이름을 붙이게 됩니다.<br>

```js
function TestObject() {
    this.one = "one";
    this.two = "two";
    this.three = "three";
}

TestObject.prototype.init = function () {
    this.one = null;
    this.two = null;
    this.three = null;
}

var myObject = new TestObject(); //객체생성
alert(myObject.one + " : " + myObject.two + " : " + myObject.three);
myObject.init(); //객체 초기화 함수 호출
alert(myObject.one + " : " + myObject.two + " : " + myObject.three);
```

TestObject 생성자 함수의 prototype에 init의 메소드를 추가시켰습니다.<br>
해당 메소드는 one, two, three의 값을 null로 초기화 해주는 역할을 해줍니다.<br>

이런 경우에 함수명 혹은 객체의 이름(key, 프로퍼티?)을 `init` 혹은 `initialize`이라고 합니다.<br>
객체같은 경우 new Object(), Object.create() 혹은 객체 리터럴 방식을 사용하여 초기화 할 수 있습니다.<br>

