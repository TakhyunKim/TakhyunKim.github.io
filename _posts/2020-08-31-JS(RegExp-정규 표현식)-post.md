---
title: "JS_RegExp(정규표현식)"
date: 2020-08-31 19:20:28 -0400
categories: Javascript RegExp
---

# RegExp 정규 표현식 (Regular Expression)

- 정규 표현식 줄여서 정규식이란 문자열에 포함된 문자 조합을 찾기 위해 사용되는 패턴입니다.

1. 정규식
- 두 가지 방법으로 정규식을 만들수 있습니다.
  
  1-1) 정규식 패턴이 계속 지속될 경우
       var re = /ab+c/;
       
  1-2) 정규식 패턴이 변경되는 경우
       var re = nw RegExp("ab+c");

2. 정규식 패턴 만들기
- 정규식 패턴은 /abc/와 같이 단순한 문자열로 만들 수 있습니다. 또한 /ab*c/ or /\d+)\.=d%/ 와 같이 특수 문자와 단순 문자열의 조합으로
  정규식 패턴을 만들 수 있습니다.
  
  2-1) 단순 문자열 패턴
       /abc/.exec("this is abc); // ["abc"] => 단순 문자열 패턴은 직접 찾고자 하는 문자들로 구성됩니다. 예를 들어, /abc/는 this is abc의 abc에 매칭됩니다.
       /abc/.exec("this is ab c); // null => 띄어쓰기로 되있기 때문에 null을 반환합니다.
  
  2-2) 특수문자를 사용한 패턴
       /ab*c/.exec("this is abbbbbce"); // ["abbbbbc"] => 하나 이상의 b를 찾거나, 단순 문자열 패턴보다 다양한 문자열을 찾기 위해 사용됩니다.
       예를 들어, /ab*c/ 패턴은 'a' 뒤에 0개 이상의 'b'와 바로 뒤에 있는 'c'가 있는 문자열을 찾습니다.
 
 3. 정규 표현식의 구성
 - /regexr/i
   
   3-1) 첫번째 "/" 시작을 의미
   3-2) "regexr"은 패턴을 의미
   3-3) 두번째 "/" 종료 기호를 의미
   3-4) "i"는 플래그를 의미 <= 플래그란? 해당 정규 표현식이 어떻게 동작할지를 나타냄 (ex) g, i, m 이 존재함)
   3-4-1) flag "i" = 대소문자를 구별하지 않고 검색한다.
   3-4-2) flag "g" = 문자열 내의 모든 패턴을 검색한다.
   3-4-3) flag "m" = 문자열의 행이 바뀌더라도 검색을 계속한다.
   
 4. 정규 표현식의 사용 예시
 
    const targetStr = 'This is a pen.';
    const regexr = /is/ig;

    // RegExp 객체의 메소드
    console.log(regexr.exec(targetStr)); // [ 'is', index: 2, input: 'This is a pen.' ]
    console.log(regexr.test(targetStr)); // true

    // String 객체의 메소드
    console.log(targetStr.match(regexr)); // [ 'is', 'is' ]
    console.log(targetStr.replace(regexr, 'IS')); // ThIS IS a pen.
    // String.prototype.search는 검색된 문자열의 첫번째 인덱스를 반환한다.
    console.log(targetStr.search(regexr)); // 2 ← index
    console.log(targetStr.split(regexr));  // [ 'Th', ' ', ' a pen.' ]
    
 5. 플래그의 사용 예시

    const targetStr = 'Is this all there is?';

    // 문자열 is를 대소문자를 구별하여 한번만 검색한다.
    let regexr = /is/;

    console.log(targetStr.match(regexr)); // [ 'is', index: 5, input: 'Is this all there is?' ]

    // 문자열 is를 대소문자를 구별하지 않고 대상 문자열 끝까지 검색한다.
    regexr = /is/ig;

    console.log(targetStr.match(regexr)); // [ 'Is', 'is', 'is' ]
    console.log(targetStr.match(regexr).length); // 3
    
 6. 패턴
<hr>
    const targetStr = 'AA BB Aa Bb';
    // 임의의 문자 3개
    const regexr = /.../;
   
    console.log(targetStr.match(regexr)); // [ 'AA ', index: 0, input: 'AA BB Aa Bb' ]
    
    "."은 임의의 문자 한 개를 의미한다. 문자의 내용은 무엇이든지 상관없다. 위 예제의 경우 "."을 3개 연속으로 패턴을 생성하였으므로 3자리 문자를 추출해야한다.
    허나 console.log로 출력을 한 결과 'AA' 하나만 출력이 되었다. 이 출력의 이유는 바로 추출을 반복하는 플래그가 없었기 때문이다.
----
    const targetStr = 'AA BB Aa Bb';

    // 임의의 문자 3개를 반복하여 검색
    const regexr = /.../g;

    console.log(targetStr.match(regexr)); // [ 'AA ', 'BB ', 'Aa ' ]
    
    플래그 'g'를 사용하여 모든 문자를 선택하도록 하였고 출력은 ... <= 임의의 문자 3개를 반복하여 검색하였으므로 위와 같이 3개의 값이 출력되었다.
----    
    const targetStr = 'AA BB Aa Bb';

    // 'A'를 검색
    const regexr = /A/;

    console.log(targetStr.match(regexr)); // 'A'
    
    이 때 대소문자를 구별하며 패턴과 일치한 첫번째 결과만 반환된다. 대소문자를 구별하지 않게 하려면 플래그 i를 사용한다.
----
    const targetStr = 'AA BB Aa Bb';

    // 'A'를 대소문자 구분없이 반복 검색
    const regexr = /A/ig;

    console.log(targetStr.match(regexr)); // [ 'A', 'A', 'A', 'a' ]
    
    플래그 ig를 사용하여 대소문자를 구분하지 않고 반복 검색하여 위 값을 출력
----
    const targetStr = 'AA AAA BB Aa Bb';

    // 'A'가 한번이상 반복되는 문자열('A', 'AA', 'AAA', ...)을 반복 검색
    const regexr = /A+/g;

    console.log(targetStr.match(regexr)); // [ 'AA', 'AAA', 'A' ]
    
    앞선 패턴을 최소 한번 반복하려면 앞선 패턴 뒤에 +를 붙인다. 이렇게 되면 A만으로 이루어진 문자열을 의마한다.
----
    const targetStr = 'AA BB Aa Bb';

    // 'A' 또는 'B'가 한번 이상 반복되는 문자열을 반복 검색
    // 'A', 'AA', 'AAA', ... 또는 'B', 'BB', 'BBB', ...
    const regexr = /[AB]+/g;

    console.log(targetStr.match(regexr)); // [ 'AA', 'BB', 'A', 'B' ]
    
    []내의 문자는 or로 동작한다. (|와 동일) 그 뒤에 +를 사용하여 앞선 패턴을 한번 이상 반복한다.
----
    const targetStr = 'AA BB Aa Bb 24,000';

    // '0' ~ '9'가 한번 이상 반복되는 문자열을 반복 검색
    const regexr = /[0-9]+/g;

    console.log(targetStr.match(regexr)); // [ '24', '000' ]
    
    숫자를 출력하는 방법이다.
</hr>
 
 7. 자주 사용하는 정규 표현식
----
    const url = 'http://example.com';

    // 'http'로 시작하는지 검사
    // ^ : 문자열의 처음을 의미한다.
    const regexr = /^http/;

    console.log(regexr.test(url)); // true
----
    특정 단어로 시작하는지 검사한다.
  
----
    const fileName = 'index.html';

    // 'html'로 끝나는지 검사
    // $ : 문자열의 끝을 의미한다.
    const regexr = /html$/;

    console.log(regexr.test(fileName)); // true
----
    특정 단어로 끝나는지 검사한다.
----
    const targetStr = '12345';

    // 모두 숫자인지 검사
    // [^]: 부정(not)을 의미한다. 얘를 들어 [^a-z]는 알파벳 소문자로 시작하지 않는 모든 문자를 의미한다.
    // [] 바깥의 ^는 문자열의 처음을 의미한다.
    const regexr = /^\d+$/

    console.log(regexr.test(targetStr)); // true
----    
 8. RegExp Constructor
  - 자바스크립트는 정규표현식을 위해 RegExp 객체를 지원한다. RegExp 객체를 생성하기 위해서는 리터럴 방식과 
    RegExp 생성자 함수를 사용할 수 있다. 일반적인 방법은 리터럴 방식이다.
----
    new RegExp(pattern[, flags])
----
  * pattern 정규표현식의 텍스트
  * flags 정규표현식의 플래그 (g,i,m,u,y)
----
    // 정규식 리터럴
    /ab+c/i;

    new RegExp('ab+c', 'i');

    new RegExp(/ab+c/, 'i');

    new RegExp(/ab+c/i); // ES6
----
    const target = 'Is this all there is?';
    const regExp = /is/;

    const res = regExp.exec(target);
    console.log(res); // [ 'is', index: 5, input: 'Is this all there is?' ]
----
    const target = 'Is this all there is?';
    const regExp = /is/g;

    const res = regExp.exec(target);
    console.log(res); // [ 'is', index: 5, input: 'Is this all there is?' ]
----
    exec 메소드는 g 플래그를 지정하여도 첫번째 매칭 결과만을 반환한다.
----
    const target = 'Is this all there is?';
    const regExp = /is/;

    const res = regExp.test(target);
    console.log(res); // true
----
    문자열을 검색하여 매칭 결과를 반환한다. 값은 불리언 값이다.
