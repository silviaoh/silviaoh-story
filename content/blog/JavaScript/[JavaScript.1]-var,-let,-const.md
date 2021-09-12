---
title: '[JavaScript.1] var, let, const'
date: 2021-09-07 19:09:82
category: 'JavaScript'
thumbnail: { thumbnailSrc }
draft: false
---

JavaScript의 변수 선언 방식에는 3가지가 존재한다. 바로 var, let, 그리고 const이다. 이 3가지의 변수 키워드는 왜 등장하게 되었을까?

오늘은 var, let, const를 각각 알아보며 이 3가지 선언 방식을 알아보는 시간을 가지자!😘

# 요약

|       | 중복 선언 | 재할당 |     scope      |
| :---: | :-------: | :----: | :------------: |
|  var  |    ⭕️    |  ⭕️   | function-level |
|  let  |    ❌     |  ⭕️   |  block-level   |
| const |    ❌     |   ❌   |  block-level   |

# 1. var

var은 variable의 약자로 ECMAScript5에서 등장한 키워드이다.
ECMAScript6에서 let, const가 추가로 등장하기 전에 JavaScript에서는 var으로 모든 변수를 선언하였다.

하지만 var은 문제가 많은 방식이다.
곧 나올 것이지만 대표적인 문제점이 hoisting과 block-level scope가 아니라는 점이다.

그러니까 var은 사용하지말고 최신의 방법인 let과 const를 많이 사용하도록 하자!

### var의 사용

```javascript
/*변수 선언*/
var one
one = 1
```

```javascript
var two = 2
```

var은 위의 코드들과 같이 먼저 선언하고 초기화하거나 변수를 선언할 때 동시에 초기화를 할 수 있다.

### var의 특징

**1. var은 중복선언이 가능하다.**

```javascript
var name = 'Steve'
console.log(name) /*Steve*/

var name = 'Jully'
console.log(name) /*Jully*/

var name
console.log(name) /*Jully*/
```

name을 중복 선언하였는데 오류가 일어나지 않고 위에서 아래로 초기화한 값대로 변수에 저장된 값이 출력된다.

만약에 name이란 변수에 초기화를 하지 않고 다시 똑같은 변수를 선언한다면 `var name;`은 무시되며 앞에서 선언한 변수에 저장된 값이 출력될 것이다.

**2. 재할당이 가능하다.**

```javascript
var name = 'Steve'
console.log(name) /*Steve*/

name = 'Jully'
console.log(name) /*Jully*/
```

var은 변수를 선언하고 값을 저장하여 초기화를 완료한 후, 값을 다시 변경하고 싶다면 다른 값으로 재할당할 수 있다.

**3. 호이스팅**
JavaScript는 다이나믹한 언어이다.
다른 언어들과는 달리 자유롭기 때문에 그만큼 조심해서 사용해야한다. let과 const가 나오기 전 변수 선언 방법인 var로 JavaScript의 크레이지한 면모를 볼 수가 있다.

프로그래밍에서는 변수를 먼저 선언하고 값을 할당하는 것이 정상적이지만,

```javascript
console.log(age) // undefined
age = 2
var age
```

var에서는 선언도 하기 전에 값을 할당할 수가 있다.🙄

심지어는 출력도 할 수 있는데, 출력을 해보면 undefined. 즉, '변수는 있지만 값이 할당되지 않은 상태네?' 라고 나온다.

이것을 var hoisting(호이스팅)이라고 한다.

정리하자면 호이스팅이란 **변수를 어디에 선언했느냐에 상관없이 항상 제일 위로 선언을 끌어올려주는 것**을 의미한다.

> javascript 파일을 작성할 때 맨 처음에 **'use strict'**를 선언하여 선언되지 않은 변수를 사용했을 때 오류가 출력되도록 한다면 우리가 생각하는 상식적인 범위 안에서 javascript를 이용할 수 있을 것이다.

### Scope

scope는 '유효범위'라는 뜻으로 이해하면 된다.
쉽게 말하면 선언된 변수를 어디까지 허용하여 그 값을 유지할 것인지를 의미한다.

var은 `function-level scope`(함수 레벨 스코프)이다.
함수 내부에 선언된 변수만 지역 변수로 한정하고 그 외에 선언된 함수는 전역 변수로 간주한다.

```javascript
var name = 'Steve'
console.log(name) //Steve*

//block-level
{
  name = 'Jully'
}

//function-level
function scopeTest() {
  var name = 'Anne'
  console.log(name)
}

scopeTest() // Anne
console.log(name) //Jully
```

name 변수는 Steve라는 값이 저장되어 있었지만 {} 안에 있는 코드로 Jully로 값이 재할당되었다.

scopeTest()안에 있는 name은 함수 안에서만 허용되는 지역 변수이기 때문에 마지막 결과값이 Jully로 출력된 것이다.

var은 함수 안에서만 지역 변수로 구분되고 그 외의 변수들은 무분별하게 전역 변수로 인식되어 메모리를 항상 차지하고 있기 때문에 성능 개선을 위해서라도 var 대신 let, const를 이용하는 것이 현명한 방법일 것 같다.

# 2. let

let과 뒤에 나올 const는 ECMAScript6에서 등장한 변수 선언 방식이다. let, const는 var로 선언하였을 때 발생하는 문제점을 해결하고 보완할 수 있다.

### let의 사용

let을 사용하여 변수를 선언할 때는 var 변수를 선언하고 초기화하는 방법과 거의 차이가 없다.

```javascript
let one
one = 1
```

```javascript
let two = 2
```

### let의 특징

**1. 중복선언이 불가능하다.**

```javascript
let name = 'Steve'
console.log(name) /*Steve*/

let name
console.log(name) /*SyntaxError 발생*/
```

var과 달리 let으로 변수를 선언할 경우, 중복으로 선언할 수 없다.

첫 번째로 변수를 선언한다면 올바르게 저장되고 출력될 것이지만, 2번 이상 똑같은 변수 이름으로 재선언한다면 SyntaxError를 발생시킨다.

**2. 재할당이 가능하다.**

```javascript
let name = 'Steve'
console.log(name) /*Steve*/

name = 'Jully'
console.log(name) /*Jully*/
```

let이 var과 유사한 점은 값의 재할당이 가능하다는 점이다. 변수를 선언하고 초기화하였을 때 var과 마찬가지로 변수의 값을 다른 값으로 변경할 수 있다.

### Scope

let은 `block-level scope`(블럭 레벨 스코프)이다.
함수도 포함하여 {}안에 선언된 변수를 지역 변수로 간주한다.

```javascript
let name = 'Steve'
console.log(name) //Steve

{
  let name = 'Jully'
  console.log(name) //Jully
}

function scopeTest() {
  let name = 'Anne'
  console.log(name)
}

scopeTest() //Anne
console.log(name) //Steve
```

함수를 포함하여 {} 안에 선언된 변수는 밖으로 나올 경우 효력이 없어지기 때문에 맨 끝에 나오는 결과는 Steve이다.

# 3. const

### const의 사용

const를 선언할 때는 앞에서 언급한 var과 let과는 다른 점이 있다.

```javascript
/*변수 선언 1*/
const one;
one = 1;
```

```javascript
/*변수 선언 2*/
const two = 2
```

2가지의 변수 선언 방법이 있는데, 과연 여기서 제대로 동작하지 않는 코드는 어떤 것일까? 바로 **1번째 코드에서 오류가 출력**된다.

const를 사용하여 변수를 선언할 때는 **반드시 초기화를 같이 해주어야 한다**. 따로 선언을 하게 되면 초기화를 해야 한다는 SyntaxError가 나타나기 때문이다.

### const의 특징

**1. 중복선언과 재할당이 불가능하다.**

```javascript
const name = 'Steve'
console.log(name) /*Steve*/

/*SyntaxError : Cannot declare a const variable twice: 'name'.*/
const name = 'Jully'
console.log(name)
```

중복 선언을 할 경우, SyntaxError가 발생한다.

```javascript
const name = 'Steve'
console.log(name) /*Steve*/

/*TypeError: Attempted to assign to readonly property. */
name = 'Jully'
console.log(name)
```

TypeError가 발생하며 값을 다시 할당하지 못한다.

### Scope

const도 let과 같이 `block-level scope`(블럭 레벨 스코프)이다.

```javascript
function scopeTest() {
  const exec = 'Anne'
  console.log(name)
}
//ReferenceError: Can't find variable: exec
console.log(exec)
```

함수를 포함한 {} 안에서만 변수가 효력을 발휘하기 때문에 함수 안에 선언된 exec 변수를 밖에서 출력할 경우 변수를 찾을 수 없다는 ReferenceError가 발생한다.
