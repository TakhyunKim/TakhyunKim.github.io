---
title: "let,const의 호이스팅과 TDZ"
date: 2020-10-24 12:20:28 -0400
categories: Javascript
---

본 내용은 구글링을 기반으로 여러 자료들을 취합한 내용입니다.

var의 호이스팅
---

``` javascript
console.log(name); // undefined
var name = 'TakhyunKim';
```

`var` 키워드는 호이스팅으로 이른바 `var name;` 선언부를 최상단으로 끌어올리게 되고<br>
`undefined`로 초기화가 됩니다. 그렇기에 에러가 발생하지 않고 undefined를 출력하게 됩니다.<br>

Javascript 인터프리터가 내부적으로 코드를 위와 같은 방식으로 처리하는 것일뿐 실제로 코드의<br>
위치가 변경되거나하진 않습니다.<br>

그렇다면 let, const의 호이스팅은??
---

``` javascript
console.log(name); // Uncaught ReferenceError: Cannot access 'name' before initialization
const name = 'TakhyunKim';
```

var와는 다르게 `ReferenceError`가 발생되는 모습입니다. `초기화 하기 전에는 name이라는 변수에 접근할수 없습니다`라는<br>
에러가 발생되었고 처음에는 이런 에러 때문에 단순히 'let, const로 선언한 변수는 호이스팅이 되지 않구나~' 라고 생각하였습니다.<br>

결론부터 말하자면 <strong>let과 const도 호이스팅이 된다</strong>입니다.<br>

```javascript
console.log(firstName); // Uncaught ReferenceError: firstName is not defined
```

위 코드를 보면 에러의 내용이 다릅니다. `firstName이라는 변수가 정의되지 않았다.`<br>
<strong>let, const 키워드로 선언한 리터럴 값은 호이스팅은 되나 특별한 이유로 인해 “초기화가 필요한 상태”로 관리되고 있다.</strong><br>
라고 간단하게 정의할 수 있습니다.

초기화가 필요한 상태?? 여기서 의미하는 초기화가 무엇일까?
---
우선 `var`로 선언한 변수의 경우 선언과 초기화가 동시에 이루어집니다. 위 예제코드에서 보셨다시피 선언과 동시에 `undefined`로 값이 초기화가 됩니다.<br>

그에 반해 `let`과 `const`의 경우 선언 후 `TDZ(Temporal Dead Zone) 구간에 들어가서<br>

<strong>선언은 되어있지만 아직 초기화가 되어있지않고 변수에 담길 값을 위한 공간이 메모리에 할당되지 않은 상태</strong><br>
라고 할 수 있습니다. 이 때 해당 변수에 접근을 하고자하면 위예제의 에러 처럼 `Cannot access '(변수명)' before initialization`<br>
에러가 뜨게 되는겁니다. 

TDZ에 대해서 정확히 알아보자
---

``` javascript
work; // ReferenceError 발생

const work = "electrical_work";
```
위 예제에서 봤던 내용처럼 호이스팅은 된 상태이지만 변수값이 초기화되기 전에 접근하려고 하면 `ReferenceError`가 발생하게 됩니다.<br>
사실상 TDZ라고 하는 구간은 `const work = "electrical_work";` 그 이전의 코드 내용의 공간을 의미합니다.

TDZ가 의미하는 바는 <strong>선언 전에 변수에 접근하는 것을 금지합니다. 선언하기 전에 아무 것도 사용하지 마세요.</strong>입니다.<br>

class도 똑같이 적용된다고 하는데 class에 대해서는 아직 다루기에 스스로 공부가 덜 된 듯하여 적용만 되는구나~ 하고 넘어가도록 하겠습니다.<br>
이밖에도 적용되는 요소가 좀 더 있는 것같은데 이 후에 좀 더 공부를 충분히 하고 다루도록 하겠습니다. 뿅-<br>

사실상 TDZ라고 하는 구간은 `const work = "electrical_work";` 그 이전의 코드 내용의 공간을 의미합니다.
