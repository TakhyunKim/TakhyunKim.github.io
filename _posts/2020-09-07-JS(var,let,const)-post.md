---
title: "var let const의 호이스팅"
date: 2020-09-07 23:02:28 -0400
categories: 변수
---

<h3> 변수의 3단계 생성과정 </h3>
  
  1. 선언 단계: 변수를 실행컨텍스트의 변수객체에 등록한다.
  2. 초기화 단계: 실행 컨텍스트에 등록된 뱐수 객체에 대한 메모리를
     할당한다. 이 단계에서 변수는 undefined로 초기화 된다.
  3. 할당 단계: undefined로 초기화된 변수에 값을 할당한다.

var 키워드로 변수를 만들 경우, 1,2단계 즉 선언단계와 초기화 단계가
동시에 이뤄집니다.
<pre>
<code>
  console.log(name) // undefined
  var name = 'seo'
</pre>
</code>
위 코드에서 var로 선언된 변수는 호이스팅되어 선언과 초기화가 동시에
이루어지기 때문에 undefined가 출력됩니다.

하지만 let 키워드는 선언단계와 초기화 단계가 분리되어 진행됩니다.
<pre>
<code>
  console.log(name) // ReferenceError: name is not defined
  let name = 'seo';
</pre>
</code>
let 키워드로 선언된 변수는 호이스팅되어 선언단계가 이뤄지지만 초기화 단계는
실제 let이 사용된 코드에 도착했을 때 이뤄집니다. 초기화 단계 이전에 변수에
접근하려하면 Reference 에러가 발생합니다.

const 변수는 let과 매우 유사하지만 차이점은 const로 선언되면 값이 상수화되어
변경이 불가능합니다. 또한 const로 선언될 경우 선언과 동시에 초기화를 해야합니다.
<pre>
<code>
  var name;
  name = 'seo'
  
  const age = 29; // 선언과 동시에 초기화 필요
  
  //const age;
  //age = '29';
</pre>
</code>

변수 Scope에 대해 설명하겠습니다.
let과 const로 선언된 변수는 블록 레벨 스코프를 가집니다. 즉 {} 내부에 변수를
선언하면 해당 블록 내부에만 생명주기를 유지합니다. 반대로 var은 함수 레벨 스코프를
가지므로, 블록 내부에 선언되어도 외부에서 접근할 수 있습니다.
<pre>
<code>
{
  let name = 'seo'  
}
console.log(name); // ReferenceError: name is not defined

{
  var age = 29;
}
console.log(name); // 29, var는 함수레벨 스코프
</pre>
</code>
