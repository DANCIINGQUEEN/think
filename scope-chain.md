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
