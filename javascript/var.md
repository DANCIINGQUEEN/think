# var
- 이 키워드로 선언된 변수는 함수 스코프 또는 전역 스코프를 가짐
- `var`로 선언된 변수가 함수 내부에서 정의되면 그 함수 내부 어디서든 접근할 수 있음을 의미. 함수 바깥에서 정의되면 어느 곳에서든 접근할 수 있다는 것을 의미


## var의 특징
1. Hoisting
   - `var`로 선언된 변수는 해당 스코프의 최상단으로 호이스팅됨
   - 선언이 스코프의 시작 부분으로 끌어올려진 것처럼 동작한다는 것을 의미하지만 초기화는 호이스팅되지 않음
   - 따라서 변수를 선언하고 초기화하기 전에 접근하려고 하면 `undefined` 값을 얻게 됨
2. Function Scope
   - `var`로 선언된 변수는 가장 가까운 함수의 스코프에 속하게 됨
   - 함수 바깥에서 선언된 경우 전역 스코프를 가지게 됨
3. 재선언 가능
   - 동일한 스코프 내에서 `var` 키워드를 사용하여 변수를 재선언하는것이 가능함
4. 전역 객체 속성
   - 전역 스코프에서 `var`로 선언된 변수는 전역 객체의 속성이 됨
   - 웹 프라우저에서 전역 객체는 `window` 객체를 의미

..`var`의 사용은 현대 javaScript에서는 권장되지 않음...

## `var`키워드를 사용한 10가지 예시
1. 기본적인 변수 선언과 초기화
```js
var name = 'Park'
console.log(name)  //Park
```
2. 함수 스코프 내에서의 사용
```js
function greet() {
  var greeting = 'Hello World'
  console.log(greeting)    
}
greet()  //Hello World
```
3. 변수 호이스팅
```js
console.log(hoistedVar)  //undefined
var hoistedVar = 'This is hoisted'
```
4. 동일한 스코프 내에서의 재선언
```js
var pet = 'cat'
var pet = 'dog'
console.log(pat)  // dog
```
5. 전역 변수로서의 선언
```js
var globalVar = 'I am global'
console.log(window.globalVar)  //I am global    (브라우저 환경에서만)
```
6. 루프 내에서의 사용
```js
for (var i = 0; i < 3; i++) {
  console.log(i)  ///0, 1, 2
}
console.log(i)  //3
```
7. 조건문 내에서의 사용
```js
if (true) {
  var conditionVar = 'Visible outside the block'
}
console.log(conditionVar)  //Visible outside the block
```
8. 함수 스코프를 이용한 변수 캡슐화
```js
function encapsulateVar() {
  var privateVar = 'I am private'
  console.log(privateVar)
}
encapsulateVar()  //I am private
console.log(privateVar)  //ReferenceError: privateVar is not defined
```
9. 함수 인자와 같은 이름의 변수 호이스팅
```js
function func(arg) {
  console.log(arg)
  var arg = 'New Value'
  console.log(arg)
}
function('Initial Value')  // Initial Value, New Value
```
10. 반복 사용하여 변수 값 변경하기
```js
var counter = 1
counter = 2
counter = 3
console.log(counter)  //3
```






































