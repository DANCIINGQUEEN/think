# let
- ES6에서 도입된 키워드
- `let`으로 선언된 변수는 block scope를 가짐

## `let`의 주요 특징
1. block scope
   - `let`으로 선언된 변수는 가장 가까운 블록 내에서만 유효함
2. 변수 호이스팅
   - `let`으로 선언된 변수도 호이스팅됨
   - 그러나 `var`와 달리 초기화 전에 접근하려고 하면 `ReferenceError`발생
   - 이는 `let`변수가 `Temporal Dead Zone(TDZ)`에 있음을 의미
     - **Temporal Dead Zone**(TDZ)이란?
       - `let`, `const` 키워드로 선언된 변수가 호이스팅되었지만, 아직 초기화되지 않아 접근할 수 없는 상태를 가리킴
       - 이 구간은 변수가 선언된 위치부터 초기화(값이 할당된) 위치까지의 코드 범위를 의미
       - TDZ의 존재는 `let`, `const`로 선언된 변수를 사용하기 전에 반드시 선언하고 초기화해야 한다는 언어의 규칙을 강제함
       - TDZ의 주요 포인트
         - 호이스팅과의 관계 : `let`, `const`로 선언된 변수는 선언 위치에서 초기화 위치까지의 범위에서 접근할 수 없음. 이 범위가 TDZ
         - 접근 제한 : 변수가 TDZ 내에 있을 때 그 변수에 접근하려고 하면 `ReferenceError`가 발생. 변수가 존재하지만 아직 사용할 준비가 되지 않음을 나타냄
         - 초기화 시점 : TDZ는 변수 선언문이 실행되어 초기화가 이루어질 때까지 지속됨. 변수에 값이 할당되는 순간 TDZ는 종료되고, 변수는 그 후부터 접근 가능해짐
       - TDZ의 목적
         - 변수를 사용하기 전에 선언되어야 한다는 프로그래 언어의 일반적인 규칙을 강화함
         - `let`, `const` 선언이 예측 가능한 스코핑 규칙을 가지도록 돕는 중요한 메커니즘
3. 재선언 금지
   - 같은 스코프 내에서 `let`을 사용하여 변수를 재선언하려고 하면 `SyntaxError`가 발생함
     ```js
     let username = "park"
     let username = "park"  //SyntaxError : Identifier 'username' has already been declared
     ```
4. 재할당 가능
   - `let`으로 선언된 변수는 재할당할 수 있음
  

## `let을 사용한 10가지 예시
1. 루프 카운터에서의 사용
```js
for (let i = 0; i < 5; i++) {
  console.log(i)   // 0,1,2,3,4
}
```

2. 조건문 내에서의 변수 선언
```js
if (true) {
  let localValue = 'accessible within this block'
  console.log(localValue)
}
```
3. 블록 스코프 변수의 한정된 사용
```js
{
  let blockScoped = 'I am only available in this block'
  console.log(blockScoped)
}
```
4. 루프 내에서의 임시 변수
```js
let names = ['Park', 'Lee', 'Hwang']
for (let i=0; i<names.length; i++) {
  let name = names[i]
  console.log(name)
}
```
5. 함수 내부에서의 임시 변수
```js
function doSomething() {
  let result = 'Some result'
  return result
}
```

6. 스위치문 내에서의 블록 스코프 함수
```js
switch (key) {
  case 1: {
    let option = 'Option 1'
    break;
  }
  case 2: {
    let option = 'Option 2'
    break;
  }
}
```
7. 모듈 스코프에서의 임시 설정
```js
let config = {
  apiKey  : '12345',
  apiBaseUrl : 'https://api.example/com'
}
```
8. 이벤트 리스너 내에서의 사용
```js
document.getElementById('myButton').addEventListener('click', function() {
  let clicked = true
})
```
9. 블록 스코프 내 임시 배열
```js
{
  let tempArray = [1,2.3]
  console.log(tempArray)
}
```
10. 동적인 속성 이름을 가진 객체의 생성
```js
let dynamicKey = 'name'
let person = {
  [dynamicKey] : 'Park'
}
console.log(person.name)    //Park
```
















































