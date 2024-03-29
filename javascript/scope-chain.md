### 자바스크립트에서 스코프 체인(scope chain)은 변수 또는 함수의 스코프가 서로 연결되어 있는 구조를 의미
### 스코프는 변수에 대한 접근성과 생명 주기를 제어하는 볌위
### 자바스크립트 엔진이 이름(변수, 함수)을 해석(resolve)할 때 사용하는 규칙
### 스코프 체인은 실행 컨텍스트(execution context)의 중요한 부분으로, 코드의 각 부분에서 어떤 변수에 접근할 수 있는지 결정

## 스코프의 종류
## Global scope
  - 코드의 최상위 레벨에 선언된 변수는 어디서든지 접근할 수 있는 글로벌 스코프를 가짐
## Local scope / Function scope
  - 함수 내부에서 선언된 변수는 해당 함수와 중첩된 함수 내부에서만 접근할 수 있음
## Block scope
  - ES6에서 도입된 let과 const는 블록 레벨 스코프를 생성
  - 중괄호 {} 로 둘러싸인 어떤 영역 내에서 선언된 변수가 그 영역 내부에서만 유효하다는 것을 의미


# 스코프 체인의 작동 원리
  1. 자바스크립트에서 함수를 호출하면, 해당 함수에 대한 새로운 실행 컨텍스트가 생성
  2. 이 실행 컨텍스트는 해당 함수의 스코프, 부모 스코프에 대한 참조(외부 렉시컬 환경의 참조), 그리고 실행에 필요한 다른 정보를 포함
  3. 함수가 변수에 접근하려고 할 때, 자바스크립트 엔진은 먼저 해당 함수의 지역 스코프에서 변수를 찾음
  4. 만약 해당 스코프 내에서 변수를 찾을 수 없다면, 스코프 체인을 따라 상위 스코프로 이동하여 변수를 찾음
  5. 이 과정은 최상의 스코프(글로벌 스코프)에 도달하거나 변수를 찾을 때까지 반복
  6. 이러한 방식으로 스코프 체인은 함수가 자신의 스코프, 부모 함수의 스콮, 그리고 글로벌 스코프에서 변수를 찾을 수 있게 해줌


```js
var globalVar = 'global'
function outer() {
  var outerVar = 'outer'
  function inner() {
    var innerVar = 'inner'
    console.log(innerVar)    // 'inner'
    console.log(outerVar)    // 'outer'
    console.log(globalVar)    // 'global'
  }
  inner()
}
outer()
```

1. inner함수는 자신의 지역 변수 innerVar에 접근할 수 있음
2. inner함수는 스코프 체인을 통해 outer 함수의 변수 outerVar와 글로벌 변수 globalVar에도 접근할 수 있음
3. 위 코드에서 스코프 체인은 inner > outer > global 순서로 형성


### 외부 렉시컬 환경의 참조(Outer Lexical Environment Reference)란?

1. Lexical Scoping
  - 렉시컬 스코핑은 변수가 코드를 작성하는 시점에서의 스코프를 기반으로 결정된다는 개념
  - 즉, 함수의 실행 컨텍스트가 아닌, 함수가 어디에 선언되었는지에 따라 변수의 스코프가 결정
  - 이러한 방식으로, 코드의 구조(문법적 위치)가 변수의 접근성을 결정짓게 됨
2. Execution Context
  - 실행 컨텍스트는 코드가 실행되기 위한 환경
  - 자바스크립트 엔진이 함수를 호출할 때마다 해당 함수에 대한 실행 컨텍스트가 생성됨
  - 이는 변수 객체(Variable Object), 스코프 체인, this 값 등을 포함
3. 외부 렉시컬 환경의 참조
  - 외부 렉시컬 환경의 참조는 해당 함수가 선언된 시점의 렉시컬 환경에 대한 참조
  - 간단히, 함수가 정의된 위치의 스코프를 의미
  - 이 참조를 통해 함수는 자신의 내부 스코프뿐만 아니라, 외부 스코프(부모 함수, 글로벌)에 접근할 수 있게 됨
#### 렉시컬 환경의 두가지 주요 구성 요소
1. Environment Record
  - 현재 컨텍스트에서 선언된 식별자(변수, 함수 선언 등)를 저장
2.  Outer Lexical Environment Reference
  - 외부 스코프에 대한 참조로, 현재 컨텍스트의 외부 스코프에 접근할 수 있게됨



### 예시 코드
```js
function outerFunction() {
 let outerVariable = 'I am outside'  //outerFunction의 지역 변수
 function innerFunction() {
    //innerFunction에서는 outerFunction의 지역 변수에 접근할 수 있음
    console.log(outerVariable)
  }
  return innerFunction
}
const myInnerFunction = outerFunction()  //outerFunction을 호출하고,  innerFunction을 반환
myInnerFunction()  //'I am outside' 출력
```
- 위 코드에서 outerFunction은 innerFunction을 내부에 정의
- innerFunction은 outerFunction의 지역 변수 ounterVariable에 접근할 수 있음
- innerFunction이 선언될 때의 렉시컬 환경에 outerVariable이 포함되어 있기 때문
- outerFunction이 실행되어 종료된 후에도 myInnerFunction을 통해 innerFunction을 호출하면 outerVariable에 접근할 수 있음
- 이는 innerFunction이 자신이 생성될 때의 렉시컬 환경을 '기억'하고 있기 때문
