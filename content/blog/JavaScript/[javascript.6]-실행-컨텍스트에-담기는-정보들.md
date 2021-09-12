---
title: '[JavaScript.6] 실행 컨텍스트에 저장되는 정보'
date: 2021-09-11 22:09:58
category: 'JavaScript'
thumbnail: { thumbnailSrc }
draft: false
---

> 이 글은 `코어 자바스크립트`를 참고하여 학습용으로 작성한 글입니다.

![](https://media.vlpt.us/images/seob/post/6e36b432-b758-4a98-889b-3d7209946fb5/image.png)

실행 컨텍스트에는 다음과 같은 3가지 정보들이 저장된다.

1. `VariableEnvironment`
2. `LexicalEnvironment`
3. `thisBinding`

## VariableEnvironment

`VariableEnvironment`에서 `Variable`은 **변수**이다. 이름만 보면 변수에 대한 정보를 저장하는 것 같지 않은가? `VariableEnvironment`에는 **현재 컨텍스트 내의 식별자들에 대한 정보 + 외부 환경 정보, 뒤에 나올 `LexicalEnvironment`의 스냅샷을 내용으로 보유하며 스냅샷을 유지한다.**

실행 컨텍스트를 생성할 때 `VariableEnvironment`에 정보를 먼저 담은 다음, 이것을 그대로 복사해서 `LexicalEnvironment`를 만들고, 이후에 수정할 때는 `LexicalEnvironment`를 주로 사용하게 된다.

## LexicalEnvironment

`environmentRecord` 객체와 `outerEnvironmentReference` 리스트로 구성되어 있다.

### environmentRecord

`environmentRecord`에는 현재 컨텍스트와 관련된 코드의 식별자 정보들이 저장된다.

여기서 코드의 식별자 정보들이란 `한 함수에 지정된 매개변수 식별자`, 함수가 있을 경우 `그 함수 자체`, `선언된 변수의 식별자` 등이다.
컨텍스트의 내부 전체를 처음부터 끝까지 쭉 훑어나가며 순서대로 수집한다.

> 전역 실행 컨텍스트는 변수 객체를 생성하는 대신 자바스크립트 구동 환경이 별도로 제공하는 전역 객체를 활용한다.

변수 정보를 수집하는 과정을 모두 마치더라도 아직 코드는 실행 전이다. 코드가 실행되기 전임에도 자바스크립트 엔진은 이미 해당 환경에 속한 **모든 변수 정보를 알고 있는 것이 된다. 즉, 단순히 이해시키자면 '자바스크립트 엔진은 코드 안의 모든 변수를 최상단으로 끌어올린 다음 코드를 실행한다(Hoisting)'** 라고 생각해도 괜찮다는 것이다.

#### **Example로 이해하는 호이스팅(Hoisting)**

#### **변수를 호이스팅 할 때**

호이스팅이란 한국말로 '끌어올리다'라고 해석된다. 변수 정보를 수집할 때 컴퓨터가 아닌 사용자의 관점에서 쉽게 이해하기 위해 나타난 용어이다. 다음의 코드를 보자.

```javascript
function a(x) {
  // 수집 대상 1(매개 변수)
  console.log(x) // [1]
  var x // 수집 대상 2(변수 선언)
  console.log(x) // [2]
  var x = 2 // 수집 대상 3(변수 선언)
  console.log(x) // [3]
}

a(1)
```

이 코드에서 x의 값을 출력하면 어떤 값들이 출력될까? 호이스팅이 되지 않았을 때는 매개변수 x의 값이 출력되므로 `[1]: 1`, 변수 x가 선언이 되었지만 값이 할당되지 않았기 때문에 `[2]: undefined`, 변수 x가 선언이 되었고 2가 할당이 되었으므로 `[3]: 2`의 결과가 출력될 것이다.

하지만 실제로는 결과가 달라진다. 바로 호이스팅(Hoisting)이 일어나기 때문이다.
이제 이해하기 쉽게 실제 코드가 실행되는 방법으로 코드를 바꿔보겠다. environmentRecord는 현재 실행될 컨텍스트의 대상 코드 내에 어떤 식별자들이 있는지만 관심이 있다. 그렇기 때문에 변수를 호이스팅할 때 변수명만 끌어올리고 할당 과정은 원래 자리에 그대로 남겨둔다.

```javascript
function a() {
  var x // 수집 대상1 : 매개변수의 변수 선언 부분
  var x // 수집 대상2 : 변수 선언 => 변수는 선언부만 끌어올린다.
  var x // 수집 대상3 : 변수 선언
  console.log(x) // [1]
  console.log(x) // [2]
  var x = 2 // 할당 부분은 호이스팅 되지 않는다.
  console.log(x) //[ 3]
}
a(1)
```

그래서 실제로는 `[1]: 1(인자 값)`, `[2]: 1(인자 값)`, `[3]: 2`가 나온다.

#### **함수를 호이스팅 할 때**

변수가 호이스팅 될 때는 변수 선언부만 호이스팅 되고 할당부는 호이스팅 되지 않는다. 함수는 어떻게 호이스팅 될까? 다음의 코드를 보자.

```javascript
function a() {
  console.log(b) // [1]
  var b = 'bbb' // 수집 대상 1(변수 선언)
  console.log(b) // [2]
  function b() {} // 수집 대상 2(함수 선언)
  console.log(b) // [3]
}
a()
```

변수 호이스팅 예제 코드에서와 마찬가지로 출력 결과를 미리 예상해보면 [1]: err or undefined, [2]: bbb, [3]: 함수 b가 출력될 것 같다. 실제로는 과연 그럴까?

a 함수를 실행하는 순간 실행 컨텍스트가 생성된다. 이 실행 컨텍스트는 당연히 a의 실행 컨텍스트이다. 이 때, 변수명과 함수 선언의 정보를 위로 끌어올린다(수집한다). 변수는 선언부와 할당부를 나눠 선언부만 위로 끌어올렸지만 함수 선언은 함수 전체를 위로 끌어올린다.

```javascript
function a() {
  var b // 수집 대상 1(변수 선언)
  function b() {} // 수집 대상 2(함수 선언)

  console.log(b) // [1]
  b = 'bbb' // 변수의 할당부는 자리에 남겨둔다.
  console.log(b) // [2]
  console.log(b) // [3]
}
a()
```

이 코드에서 한 가지만 수정하자면, 호이스팅이 끝난 상태에서의 함수 선언문은 함수명으로 선언한 변수에 함수를 할당한 것처럼 여길 수 있다.

```javascript
function a() {
  var b // 수집 대상 1(변수 선언)
  var b = function b() {} // change!

  console.log(b) // [1]
  b = 'bbb' // 변수의 할당부는 자리에 남겨둔다.
  console.log(b) // [2]
  console.log(b) // [3]
}
a()
```

변수 정보를 수집했으니 이제 코드를 실행할 차례이다.

```javascript
function a() {
  /*변수 b를 선언한다.
  이 때, 메모리에서는 변수를 저장할 공간을 미리 확보하고, 확보한 공간의 주소값을 변수 b에 연결한다.*/
  var b
  /*다시 변수 b를 선언. 함수 b를 선언된 변수 b에 할당한다.
  하지만 이미 선언된 변수 b가 있으므로 선언 과정은 무시한다.
  함수는 별도의 메모리에 담길 것이고, 그 함수가 저장된 주소값을 b와 연결된 공간(위에서 확보한 공간)에 저장한다. 이제 변수 b는 함수를 가리키게 된다.*/
  var b = function b() {}
  console.log(b) // 함수 b 출력!
  /*변수 b에 'bbb'를 할당하라. 
  b와 연결된 메모리 공간에는 이미 함수가 저장된 주소값이 담겨있었는데 이걸 'bbb'가 저장된 주소값으로 덮어쓴다. 
  이제 변수 b는 'bbb'를 가리킨다.*/
  b = 'bbb'
  console.log(b) // 'bbb'
  console.log(b) // 'bbb'
}
a()
```

#### **Example로 이해하는 함수 선언문 vs 함수 표현식**

변수 호이스팅은 선언부만 호이스팅되고 할당부는 그 자리에 그대로 남겨둔다. 여기서 함수 선언문과 함수 표현식의 차이가 발생하게 된다.

```javascript
console.log(sum(1, 2))
console.log(multiply(3, 4))

function sum(a, b) {
  // 함수 선언문
  return a + b
}

var multiply = function(a, b) {
  // 함수 표현식
  return a * b
}
```

sum 함수처럼 function 정의부만 존재하고 별도의 할당 명령이 없는 것을 `함수 선언문`이라고 하고, multiply 함수처럼 정의한 function을 별도의 변수에 할당하는 것을 `함수 표현식`이라고 한다. environmentRecord의 정보 수집 과정에서 발생하는 호이스팅을 살펴보자.

```javascript
// 메모리 공간을 확보하고 확보된 공간의 주소값을 sum에 연결한다.
var sum = function sum(a, b) {
  // 함수 선언문은 전체를 호이스팅한다.
  return a + b
}
// 다른 메모리 공간을 확보하고 그 공간의 주소값을 변수 multiply에 연결한다.
/* 그 후에 sum 함수를 또 다른 메모리 공간에 저장하고, 그 주소값을 앞서 선언한 변수 sum의 공간에 할당한다.
이로써 변수 sum은 함수 sum을 바라보는 상태가 된다.*/
var multiply // 변수는 선언부만 호이스팅 된다.
//sum을 실행한다.
console.log(sum(1, 2))
// multiply에는 값이 할당되어있지 않기 때문에 multiply is not a function이라는 에러 메시지가 출력될 것이다.
console.log(multiply(3, 4))
// 이 줄도 앞의 에러로 인해서 실행되지 않은 채 런타임이 종료된다.
multiply = function(a, b) {
  // 할당부는 호이스팅 되지 않는다.
  return a * b
}
```

위처럼 함수 선언문은 함수 전체를 호이스팅 하는 반면 함수 표현식은 변수에 함수가 할당되어 있는 것이기 때문에 선언부만 호이스팅되고 할당부는 끌어올려지지 않는다. 여기서 결과의 차이가 발생하는 것이다.

### outerEnvironmentReference

- 연결 리스트 형태를 띈다.
- 함수가 선언될 당시의 LexicalEnvironment의 정보를 참조한다.

#### **Scope와 Scope Chain이란?**

- 식별자에 대한 유효범위이다.
- ES6에서 스코프는 함수에 의해서 또는 블록에 의해서 생성된다.
- 식별자의 유효범위를 안에서부터 바깥으로 차례로 검색해 나가는 것을 `스코프 체인`이라고 한다.

#### **Example로 이해하는 스코프 체인**

```javascript
1 var a = 1;
2 var outer = function() {
3   var inner = function() {
4     console.log(a);
5     var a = 3;
6   }
7   inner();
8   console.log(a);
9 }
10 outer();
11 console.log(a);
```

**활성화 컨텍스트: 전역**

- 시작 : 전역 컨텍스트가 활성화됨.
  - 전역 컨텍스트의 LexicalEnvironment에 들어가는 내용.
    - environmentRecord에는 { a(전역 변수), outer(변수) } 형태로 저장된다.
    - outerEnvironmentReference에는 아무것도 담기지 않는다.
- a = 1 할당
- outer에 함수 할당

---

**활성화 컨텍스트: outer**

- `10번째 줄`: outer 함수 호출. 전역 컨텍스트 코드 일시 중단됨. outer 실행 컨텍스트가 활성화됨.
- `2번째 줄`
  - environmentRecord에는 { inner } 형태로 저장된다.
  - outerEnvironmentReference에는 **outer 함수가 선언될 당시의 LexicalEnvironment가 담긴다.** 형태는 `{ 실행 컨텍스트의 이름(직전에 활성화 된), environmentRecord 객체(직전에 활성화된) }`로 저장된다. 그러므로 outer 실행 컨텍스트의 outerEnvironmentReference에는 [ GLOBAL, {a, outer} ] 형태로 저장된다.
- outer 스코프에 있는 변수 inner에 함수를 할당함.

---

**활성화 컨텍스트: inner**

- `7번째 줄` : inner 함수 호출함. outer 실행 컨텍스트가 일시중단되고 inner 실행 컨텍스트가 생성되고 활성화됨.
- `3번째 줄`
  - environmentRecord에는 { a(inner 함수 안의 변수) } 형태로 저장된다.
  - outerEnvironmentReference에는 **inner 함수가 선언될 당시의 LexicalEnvironment**가 저장된다. 그러므로 [ outer, { inner } ] 형태로 저장된다.
- `4번째 줄` : a는 undefined이다. 현재 활성화 상태인 inner 컨텍스트의 `environmentRecord`에 a가 발견됐지만 할당된 값이 없기 때문이다.
- `5번째 줄` : inner scope에 있는 a에 3을 할당함
- inner 함수 실행이 종료되고 inner 실행 컨텍스트가 콜 스택에서 제거된다. 일시중단되었던 outer 실행 컨텍스트가 다시 활성화되며 코드 8번째 줄이 실행된다.

---

**활성화 컨텍스트: outer**

- 자바스크립트 엔진이 현재 활성화된 outer 컨텍스트의 environmentRecord를 확인한다. a가 있는지 확인하고 없으면 현재 실행 컨텍스트의 outerEnvironmentReference에 있는 environmentRecord로 넘어가는 식으로 계속해서 검색한다. 여기서는 전역 LexicalEnvironment에 a가 있으므로 그 a에 저장된 값을 반환한다.
- outer 함수 실행 종료되고 outer 실행 컨텍스트가 콜 스택에서 제거된다. 일시중단되었던 전역 컨텍스트가 다시 활성화되면서 코드 11번째 줄을 실행한다.

---

**활성화 컨텍스트: 전역**

- 현재 활성화 상태인 전역 컨텍스트의 environmentRecord 검색하여 a가 있기 때문에 a에 저장된 1을 출력한다.
- 코드의 실행이 완료되었기 때문에 전역 컨텍스트가 콜 스택에서 제거되고 종료된다.

![](https://images.velog.io/images/silviaoh/post/cea855b6-020e-4b70-ac3f-89d7c82fdf13/image.png)

## ✅ 정리

- 실행 컨텍스트 객체는 활성화되는 시점에 `VariableEnvironment`, `LexicalEnvironment`, `thisBinding`의 세 가지 정보를 수집한다.

---

- `VariableEnvironment`는 **현재 컨텍스트 내의 식별자 정보 + 외부 환경 정보, LexicalEnvironment의 스냅샷을 내용으로 보유한다.**
- VariableEnvironment와 LexicalEnvironment는 동일한 내용으로 구성된다.
- 둘의 **차이점**은 VariableEnvironment는 초기 상태를 유지하는 반면에 LexicalEnvironment는 함수 실행 도중에 변경되는 사항이 즉시 반영된다는 것이다.
- `LexicalEnvironment`의 environmentRecord는 `매개변수명`, `변수의 식별자`, `선언한 함수의 함수명` 등을 수집하여 저장하는 **객체**이다.
- `호이스팅(Hoisting)`은 코드 해석을 좀 더 수월하게 하기 위해 environmentRecord의 수집 과정을 추상화한 개념이며, 실행 컨텍스트가 관여하는 코드 집단의 최상단으로 이를 '끌어올린다'고 해석하는 것이다.
- **변수 호이스팅**은 선언부만 코드 최상단으로 끌어올리고 할당부는 원래 자리에 남아있는다.
- **함수 선언문**은 function 정의부만 존재하고 별도의 할당 명령이 없는 것이며, **함수 표현식**은 정의한 함수를 변수에 할당하는 것이다.

---

- `LexicalEnvironment`의 outerEnvironmentReference는 바로 직전 컨텍스트의 LexicalEnvironment의 정보를 참조하는 연결 리스트이다.
- **스코프**는 식별자에 대한 유효범위이고, 스코프 체인은 스코프(유효 범위)를 안에서부터 바깥으로 차례대로 검색해나가는 것을 말한다.
- **outerEnvironmentReference의 형태**는 [ 컨텍스트의 이름, environmentRecord 객체 ]이다.
- 자바스크립트 엔진은 변수가 있는지 검색할 때 현재 활성화된 실행 컨텍스트의 L.E(LexicalEnvironment)의 environmentRecord를 먼저 검색하고 없을 경우 outerEnvironmentReference에 있는 environmentRecord를 검색한다.
