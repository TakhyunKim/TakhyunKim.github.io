---
title: "개념정리 - this"
date: 2020-10-27 15:10:28 -0400
categories: Javascript
---

this
---
`this`는 함수를 호출할 때 결정되는 것이다. 라고 생각하시면 됩니다.<br>
함수를 어떤 방식으로 호출하느냐에 따라 this가 가르치는 객체가 달라지는 것이므로,<br>
함수 호출 방식에 따른 결과를 하기에 내용에서 확인해 보겠습니다.<br>

전역공간에서의 this
---
전역 공간에서의 `this`는 전역 객체를 가르킵니다.

```js
console.log(this); // window 객체
console.log(window); // window 객체
console.log(this === window); // true
````

```js
var name = "tak";

function foo () {
  console.log(this.name);
}

foo(); // tak
```
첫 예제에서 전역 공간에서 this를 콘솔에 찍었을 경우 window 객체를 출력하게됩니다.<br>
두번째 예제에서 함수 foo를 실행시키게 되고 함수 내의 `console.log(this.name);`를<br>
실행하게 되면 전역 공간에 있는 name의 값인 'tak'을 출력하게 됩니다.<br>

```js
var name = "tak";

var brother = {
  name : "tae",
  foo : function () {
    console.log(this.name);
  }
};

var obj = brother.foo;

obj(); // tak (일반함수 실행 방식)
brother.foo(); // tae (메소드로 호출했을 경우 dot notation)
```
`obj();`와 `brother.foo();` 결과값이 서로 다르게 출력됩니다.<br>
분명 변수 obj에도 brother.foo라는 값이 할당이 되었으므로 결과값이<br>
동일하게 출력될거 같다는 생각과 다른 결과입니다.<br>

이는 함수를 호출하는 방식이 서로 다르기에 발생한 차이점입니다.<br>
obj를 함수로 출력하였을 때는 `일반 실행 함수 방식`으로 실행되었습니다.<br>
obj에 담긴 내용은 단순히 `console.log(this.name);`가 담긴 함수입니다.<br>
그렇기 때문에 `obj();`과 같은 형태로 출력했을 때의 this는 전역 공간을 가르키게 되며,<br>
`tak`을 출력하게 됩니다.<br>

반면에 `brother.foo();`과 같은 형태로 출력했을 경우에는 다음에 다룰 내용이지만,<br>
설명하자면 이때의 this는 "." 앞의 brother 객체를 가르키며 이 때 name인 `tae`를 출력하게 됩니다.<br>
(만약 'use strict' strict 모드에서 실행했을 경우 this는 전역객체가 아닌 undefined가 됩니다.<br>
해당 내용은 다른 파트에서 다루도록 하겠습니다.)<br>

메소드로 호출했을 경우
---
위 예제에서 `brother.foo();`와 동일합니다. <br>

함수를 실행시키는 방법에는 여러가지가 있습니다. 그중에서 가장 일반적인 방법 두 가지는<br>
1. 함수로서 호출하는 경우<br>
2. 메소드로서 호출하는 경우<br>

위 두 가지입니다. 이 둘을 구분하는 유일한 차이는 `독립성`에 있습니다.<br>
<strong>함수는 그 자체로 독립적인 기능을 수행하는 반면, 메소드는 자신을 호출한 대상 객체에 관한 동작을 수행합니다.</strong><br>
이러한 특징을 기반으로 `this`에 다른 값(객체)를 부여할 수 있습니다.<br>
``` js
var func = function (x) {
  console.log(this, x);
};
func(1); // window {..} 1 => 함수로서의 호출

var obj = {
  method: func
};

obj.method(2); // {method: f} 2 => 메소드로서의 호출
```

첫번째 예제에서 func라는 변수에 익명함수를 할당했습니다.<br>
함수를 호출했을 때 this는 전역객체를 가르키게 됩니다.<br>

두번째 예제에서는 obj라는 객체에서 method라는 key 값으로 첫번째 예제의 변수인 func를<br>
할당하였습니다. 그리고 호출했을 때의 this는 객체 obj를 가르키게 됩니다.<br>

두번째 예제가 바로 `메소드로서의 호출 dot natation`입니다.<br>
어떤 함수를 표기할 때 그 함수 이름(프로퍼티) 앞에 객체가 명시되어 있는 경우에는 메소드로<br>
호출한 것이며, 이 때 메소드 내에 this는 dot 앞의 객체를 가르키게 됩니다.<br>

```js
var obj1 = {
  outer: function () {
    console.log(this); // (1)

    var innerFunc = function () {
      console.log(this); // (2) (3)
    }
    innerFunc();
    
    var obj2 = {
      innerMethod: innerFunc
    };
    obj2.innerMethod();
    
  }
};

obj1.outer();
```
생각보다 긴 예제입니다. 위 예제에서의 각 this값은 무엇일까요??<br>

제일 처음 해당 함수를 호출하는 부분을 살펴보겠습니다.<br>
`obj1.outer();` 함수를 메소드로서 호출하였습니다.(dot notation)<br>
obj1이라는 객체의 outer 프로퍼티의 값을 확인해보니 익명함수가 담겨있습니다.<br>
`console.log(this);`를 하게 될 경우에는 객체 obj1 정보인 `{outer: f}`가 출력됩니다.<br>

그리고 `innerFunc();`를 호출하게 됩니다. 이 때는 그냥 함수를 호출한 `일반함수 실행방식`입니다.<br>
그렇기에 이 때의 this는 전역 객체를 가르키며 `window {------}`를 출력하게 됩니다.<br>

그리고 obj2를 읽으면서 `obj2.innerMethod();`이라는 코드를 만나 출력하게 됩니다.<br>
이때는 처음과 같이 메소드로서의 호출이므로 `this는 obj2를 가르키게 됩니다.`<br>
프로퍼티의 값을 보니 innerFunc을 다시 호출하였습니다. console.log(this)를 실행하게 되므로<br>
값은 obj2의 내용인 `{innerMethod: f}`이 출력되게 됩니다.<br>

이를 토대로 최종적으로 정리하면<br>
<strong>해당 함수를 호출하는 구문 앞에 점 또는 대괄호 표기가 있는지 없는지가 관건입니다.</strong><br>


생성자 함수에서의 this
---
생성자 함수는 어떤 공통된 성질을 지니는 객체들을 생성하는 데 사용하는 함수입니다.<br>
객체 지향 언어에서는 클래스, 클래스를 통해 만든 객체를 인스턴스라고 합니다.<br>

```js
// 하기의 구문은 블로그에서 그대로 퍼왔습니다.(개인 공부를 위해.. 빌려쓰겠습니다..)
function NewObject(name, color) {
  this.name = name
  this.color = color
  this.isWindow = function() {
    return this === window
  }
}

const newObj = new NewObject('nana', 'yellow')
console.log(newObj.name) // nana
console.log(newObj.color) // yellow
console.log(newObj.isWindow()) // false

const newObj2 = new NewObject('didi', 'red')
console.log(newObj2.name) // didi
console.log(newObj2.color) // red
console.log(newObj2.isWindow()) // false
```

new를 이용하여 새로운 객체를 생성했을 경우 생성자 함수 내의 this는 new를 통해 만들어진 새로운 변수가 됩니다.<br>
`newObj`, `newObj2`는 같은 생성자 함수로 만들어진 객체이지만 완전히 별도의 객체이기 때문에<br>
각 객체의 속성들은 서로 관련이 없습니다. 만약 new가 빠지게 되면 어떻게 될까요?<br>

```js
const withoutNew = NewObject('nana', 'yellow')
console.log(withoutNew.name) // error
console.log(withoutNew.color) // error
console.log(withoutNew.isWindow()) // error
```

new가 없으면 일반적인 함수 실행과 동일하게 동작하므로, `NewObject` 함수내의 this는 `window` 객체가 됩니다.<br>
(일반 함수 실행 방식이므로)<br>
하지만 `withoutNew`가 함수 실행의 결과값이 할당되므로 각 property를 가져올 수 없습니다.<br>
(위 내용에 경우가 궁금했고 그 궁금증을 완벽히 해소해주는 예제였습니다. 감사합니다.)<br>

또 다른 예제를 살펴보겠습니다. 하기의 예제는 생성자 함수와는 관련이 없습니다.<br>

```js
const person = {
  name: 'john',
  age: 15000,
  nickname: 'man from earth',
  getName: function() {
    return this.name
  },
}
console.log(person.getName()) // john

const otherPerson = person
otherPerson.name = 'chris'
console.log(person.getName()) // chris
console.log(otherPerson.getName()) // chris
```
생성자 함수와 크게 다르지 않습니다. 다만 눈여겨 볼 점은 `otherPerson.name`을 `chris`로 설정한 뒤<br>
`person.getName()`을 호출하면 그 결과는 `chris`입니다.<br>
그 이유는 블로그에서의 내용은 otherPerson은 person의 레퍼런스 변수이므로 하나(otherPerson)를 변경하면<br>
다른 하나(person)도 변경됩니다. <br>
제 개인적인 해석을 해보겠습니다. <br>
```js
var a = {
    name: "tak"
};

var b = a;

b.name = "tae";

console.log(a); // {name: "tae"}
```
조금은 쉬운 예제를 가져왔습니다. 변수 a에는 name 프로퍼티를 가지고 있는 객체가 할당되어있습니다.<br>
이후 변수 b에 a를 그대로 할당하였습니다.<br>

이 때 변수 a 그리고 b에는 객체 그 자체의 값이 아닌 객체의 주솟값이 담겨져 있습니다. <br>
변수 b에 a를 할당할 때 새로운 객체를 할당하는 것이 아닌 변수 a의 객체의 정보가 담겨져있는 주솟값인<br>
예를 들면 1000이라는 주솟값이 a와 b에 할당되어있는 것입니다.<br>

이후 `b.name = "tae";`라는 코드를 통해 b의 프로퍼티 값을 변경하게 되면 주솟값은 변경되지 않습니다.<br>
단순히 주솟값을 따라 그 내부의 객체의 프로퍼티 값을 변경하게 됩니다.<br>

결국 이와 같은 과정으로 인하여 a와 b는 같은 주솟값을 가르키게 되고, 둘 중에서 어떤 변수에서라도<br>
객체의 내용을 수정하게 되면 이 수정된 내용은 공유하게 되는 것입니다.<br>

이같은 현상을 피하기 위해서 `Object.assign()`메소드를 활용하여 아예 객체를 분리하는 방식이 있다고 합니다.<br>

call, apply, bind에서의 this
---
배열에 배열만의 메소드가 있고, 객체에도 메소드가 있듯이 함수에도 함수만의 메소드가 있습니다.<br>
소제목의 call, apply, bind가 그 메소드 중 하나입니다.<br>

위 메소드들은 this의 값을 지정할 수 있다는 특징을 가지고 있으며 아래 내용에서 이를 다룰 것입니다.<br>
``` js
function family () {
  console.log(this.name);
}

var nameFunc = {
  name: "tak"
};

// call 메소드를 통해 함수를 실행
family.call(nameFunc); // tak
```

이와 같이 call을 이용하여 호출하게 되면 첫번째 인자로 받은 객체가 this가 됩니다.<br>
더불어 call은 받을 수 있는 인자의 수에 제한이 없으며, 두번째 인자부터는 함수의<br>
인자로서 활용할 수 있게 됩니다.<br>

apply도 역시 똑같은 기능을 하고 있지만 받을 수 있는 인자가 2개로 한정되어 있으며,<br>
두번쨰 인자는 배열의 형태로 작성되고 배열의 요소가 함수의 인자로서 활용되게 됩니다.<br>

bind메소드는 <strong>새로운 함수를 반환하고, 변수에 담기는 값이 함수가 됩니다.</strong><br>
이 메소드 역시 첫번째 인자를 this로 설정하게 됩니다.(인자의 수에 대한 제한은 없습니다.)<br>

생성자 함수 안에서의 함수에서의 this(블로그 참고)
---
```js
function Family(firstName) {
  this.firstName = firstName;
  const names = ['bill', 'mark', 'steve'];
  names.map(function(lastName, index) {
    console.log(lastName + ' ' + this.firstName);
    console.log(this);
  });
}
const kims = new Family('kim')
// bill undefined
// window
// mark undefined
// window
// steve undefined
// window
```
보면서 굉장히 뭔가.. 싶었던 예제였습니다. 하기에 내용을 보겠습니다.<br>
생성자 함수 안에서 `map` 메소드를 호출합니다. 이를 통해 firstName과 배열에 담겨져 있는 내용을<br>
조합 후 출력하려는 의도가 보입니다.<br>

막상 출력했을 때에는 fisrtName이 들어갈 공간에 undefined가 출력되게 됩니다.<br>
기존 의도대로 였다면 kim이 들어가야하는 자리에 말이죠.. 흠...(사실 이해가 전혀 안갔음)<br>

map을 이용한 내용에서 this를 사용한게 문제가 된 듯합니다.<br>
map 메소드를 호출했을 당시 name에 아무런 바인딩이 없었습니다. <br>
이 말인 즉슨 `일반함수 실행방식`으로 진행되었으며 이에 따라 this는 자동으로 전역 객체를 가르키게 됩니다.<br>
그렇기에 undefined가 출력되었던 것입니다.<br>

이를 해결하기 위해 this를 직접적으로 상수에 지정하는 방식이 있습니다.<br>
```js
function Family(firstName) {
  this.firstName = firstName;
  const names = ['bill', 'mark', 'steve'];
  const that = this;
  names.map(function(value, index) {
    console.log(value + ' ' + that.firstName);
  });
}
const kims = new Family('kim');
// bill kim
// mark kim
// steve kim
```
정상적으로 출력됩니다. Family에서의 this의 내용을 아예 변수 that에 담아서<br>
사용을 했으므로, 이를 사용하게 되면 자동으로 Family.firstName을 가르키게 됩니다.<br>
그러나 매번 이런 방식으로 상수를 만드는 것은 번거로운 과정입니다.<br>
다른 방식을 보겠습니다 <br>

```js
function Family(firstName) {
  this.firstName = firstName;
  const names = ['bill', 'mark', 'steve'];
  names.map(
    function(value, index) {
      console.log(value + ' ' + this.firstName);
    }.bind(this)
  );
}
const kims = new Family('kim');
```

bind(this)를 통해 묶어주어 해결했습니다만, 역시 뭐가 또 붙으니 껄끄럽습니다.<br>
그래서 이와 같은 현상을 확실하게 해결해주는 방식이 있습니다.<br>

화살표 함수에서의 this
---
```js
function Family(firstName) {
  this.firstName = firstName;
  const names = ['bill', 'mark', 'steve'];

  names.map((value, index) => {
    console.log(value + ' ' + this.firstName)
  });
}
const kims = new Family('kim');
```
화살표 함수는 함수를 선언할 때 this에 바인딩할 객체가 정적으로 결정된다. <br>
동적으로 결정되는 일반 함수와는 달리 화살표 함수의 this 언제나 상위 스코프의 this를 가리킨다.<br>

이 말인 즉슨 쉽게 설명하자면 화살표 함수에서는 this라는 것이 없습니다.라고 생각하면 편합니다.<br>

기본적으로 함수를 선언하게 되면 arguments와 같이 this라는 내용이 자동적으로 생기게 되는데<br>
화살표 함수는 일반적인 함수와 달리 this가 없기 때문에<br>
화살표 함수에서 this를 사용하게 되면 "난 얘에 대한 정보를 몰라 그러니깐 상위 스코프에서 찾아보자"<br>
라고 하며, 상위 스코프를 찾게 되는데 이 때 일반적인 함수에서는 this가 존재하므로, 그 this를 참고하게 됩니다.<br>

최종
---
무진장 헷갈린다... 정리하면서 몇 번을 읽어봐야 겨우 이해가 된다...ㅠㅡㅠ

