---
title: "코테-소수 찾기 Level 2"
date: 2020-10-05 16:37:28 -0400
categories: Javascript
---

문제 설명
---
한자리 숫자가 적힌 종이 조각이 흩어져있습니다. 흩어진 종이 조각을 붙여 소수를 몇 개 만들 수 있는지 알아내려 합니다.

각 종이 조각에 적힌 숫자가 적힌 문자열 numbers가 주어졌을 때, 종이 조각으로 만들 수 있는 소수가 몇 개인지 return 하도록 solution 함수를 완성해주세요.

제한사항
---
numbers는 길이 1 이상 7 이하인 문자열입니다.
numbers는 0~9까지 숫자만으로 이루어져 있습니다.
013은 0, 1, 3 숫자가 적힌 종이 조각이 흩어져있다는 의미입니다.

입출력 예
---
numbers	return
17	3
011	2

입출력 예 설명
---
예제 #1
[1, 7]으로는 소수 [7, 17, 71]를 만들 수 있습니다.

예제 #2
[0, 1, 1]으로는 소수 [11, 101]를 만들 수 있습니다.

11과 011은 같은 숫자로 취급합니다.

코드
---
``` javascript
function solution(numbers) {
    const decimalNumbers = getDecimalArr(10 ** numbers.length); // 하기 소수를 얻을 수 있는 함수를 호출, 값 할당
    const paperNumbers = numbers.split("").map(v => Number(v)); // 배열 내 문자열을 분리 후 숫자로 변경
    
    let answer = 0;
    decimalNumbers.forEach(v => {
       if (CorrectPaperNumber(paperNumbers, v)) {
           answer++;
       } 
    });
    return answer;
}

// 기존 종이 조각의 숫자 조합식
const CorrectPaperNumber = (paperNumbers, target) => { // target은 소수값이 들어온다.
    const targetArr = target.toString().split("").map(v => Number(v)); // 소수값을 숫자로 배열화
    const CopyPaperNumbers = paperNumbers.slice(); // 기존 문자열을 분리하고 숫자로 변경된 배열을 얕은 복사
    
    while(true) {
        const paperNumbers = CopyPaperNumbers.shift(); // while문이 반복될 때마다 앞의 요소의 값을 재 할당
        
        if (targetArr.length === 0) {
            return true;
        }
        if (targetArr.includes(paperNumbers)) { // bool값으로 반환 되고, 소수값내에 종이숫자가 포함되어 있는지를 확인
            const index = targetArr.findIndex(v => v === paperNumbers);
            targetArr.splice(index, 1);
            continue;
        }
    }
}

// 소수 함수
const getDecimalArr = (n) => {
    let decimalNumbers = Array(n + 1).fill(0).map((v, i) => v = v + i); // 0부터 n까지의 배열 생성
    
    for (let i = 2; i <= Math.sqrt(n); i++) {
        if (decimalNumbers[i] === 0) {
            continue;
        }
        for (let j = i + i; j < n + 1; j += i) {
            decimalNumbers[j] = 0;
        }
    }
    return decimalNumbers.filter(v => v !== 0).slice(1); // 제일 첫 값 0을 제거하고 slice(1)에 의해 1이 제거 - 2부터 시작
}
```

풀이
---
일단 정말 어려웠고, 한 부분에서 도무지 해답을 찾을 수없어 외부의 코드를 참고하여 작성하였습니다.
(사실 컨닝 수준)
처음 문제를 해결하고자 해서 찾은 방식은 하기의 내용과 같습니다.
1. 일정 숫자까지의 숫자를 배열로 생성 후 에라토스테네스의 체를 사용하여 소수만을 반환하는 함수 생성
2. (문제였던 파트) 문제에서 말한 종이로 조합된 숫자를 만든다.
3. 1과 2에서 공통된 숫자가 있으면 count++하여 반환한다.
위 3가지의 함수를 통해 문제를 해결하고자 했으나, 2번인 종이 내의 요소들로 각각의 숫자로 만드는 과정을
아무리 고민해도 해결이 되지 않아 외부의 코드를 보고 이해하여 사용하였습니다.
(참조 블로그: https://woomin.netlify.app/tdd/2020/06/2020-06-07-tdd/) <= 감사합니다...
이해했던 내용은 코드 내의 주석으로 작성하였습니다.

소요 시간
---
6시간 30분
