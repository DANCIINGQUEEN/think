# Hoisting
- JavaScript에서 변수와 함수 선언을 코드의 상단으로 끌어올리는 것처럼 동작하는 특성
- 실행 컨텍스트의 생성 단계에서 메모리에 변수와 함수 선언을 저장하는 방식 때문에 발생
- 호이스팅은 변수의 선언과 함수 선언 모두에 영향을 미치지만, 변수의 초기화와 함수 표현식에는 다르게 작용

## 변수 호이스팅
- `var` 키워드로 선언된 변수 : `var`로 선언된 변수는 호이스팅되어 선언부가 해당 스코프의 최상단으로 끌어올려짐
- 하지만 초기화는 호이스팅되지 않아 변수에 접근하면 `undefined` 반환
```js
console.log(myVar)    //undefined
var myVar = 5
```
- `let`, `const` 키워드로 선언된 변수 : 이들도 호이스팅되지만 `var`와 달리 TDZ 내에서 접근할 수 없음
- 이 구간에서 변수에 접근하려 하면 `ReferenceError` 반환
```js
console.log(myLet)  // ReferenceError : Cannot access 'myLet' before initialization
let myLet = 5
```

## 함수 호이스팅
- 함수 선언 : 함수 선언은 호이스팅되어 코드의 상단으로 끌어올려짐. 이 때문에 함수를 선언하기 전에 호출할 수 있음
```js
hello()  // Hello, world
function hello() {
  console.log('Hello, world')
}
```
- 함수 표현식 : 함수 표현식은 호이스팅되지 않음. 함수 표현식은 변수에 할당된 함수를 의미하며, 변수 호이스팅의 규칙을 따름
- 즉 `var`로 선언된 변수는 `undefined`로 초기화되고, `let`, `const`로 선언된 변수는 TDZ에 있게됨
```js
hello()  //TypeError: hello is not a function
var hello = function() {
  console.log("Hello, world")
}
```
