---
title: "Javascript_Prototype"
date: 2017-10-20 08:26:28 -0400
categories: Prototype | 오버라이드 개념
---

<h3> 오버라이드 </h3>

  메서드 오버라이드(override)는 자식 클래스에서 부모 클래스의 기능(method)을 재정비할 때 사용하는 기능입니다.

  사용하는 경우는 하기 두 가지의 경우입니다.
  1. 부모 클래스의 기능을 사용하지 않고 자식 클래스에서 구현한 기능을 사용하고 싶은 경우
  2. 부모 클래스의 기능을 자식 클래스에서 확장하고 싶은 경우

  <pre>
  <code>
  var a = {
      method1: function() { return 'a1' }
  };

  var b = {
      __proto__: a,
      method1: function() { return 'b1' }
  };

  var c = {
      __proto__: b,
      method3: function() { return 'c3' }
  };

  a.method1() // 'a1'
  c.method1() // 'b1'
  </pre>
  </code>

   c 객체에서 method1() 메서드를 실행하면 프로토타입 룩업을 통해 c에서 b로 이동하고 b에 이미 해당 메서드가 있기 때문에
   a 까지 안 올라가고 b의 method1()이 실행된다. 자바스크립트에서는 이런 상황을 a의 method1() 메서드를 b가 오버라이드
   했다고 한다.
