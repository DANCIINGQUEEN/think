# const
- JavaScript에서 상수를 선언하기 위해 사용되는 키워드
- 이 키워드로 선언된 변수는 블록 스코프를 가지며, 선언 시에 반드시 초기화해야됨
- `const`로 선언된 변수의 값은 재할당을 통해 변경될 수 없음
- 변수가 가리키는 메모리 주소를 변경할 수 없음을 의미하지만, 변수가 객체나 배열을 가리키는 경우 객체 내부나 배열 내부의 값을 변경할 수 있음


## `const`의 특징
1. Block Scope
   - 변수는 선언된 블록({}로 둘러싸인 영역) 내에서만 접근 가능함
2. 재할당 금지
   - 한 번 할당된 값을 변경할 수 없음
   - 변수에 새로운 값을 할당하려고 하면 TypeError가 발생함
3. 선언 시 초기화 필수
   - `const`로 선언된 변수는 선언과 동시에 초기화되어야함
   - 초기화 없이 선언만 하려고 시도하면 SyntaxError 발생
4. 객체 내부의 변경 가능
   - `const`로 선언된 객체의 속성은 변경할 수 있음
   - `const`는 변수에 할당된 데이터의 불변성을 보장하지 않고, 단지 변수가 참조하는 메모리 주소의 불변성만을 보장함

## `const` 사용의 10가지 예시
1. 기본 상수 선언
```js
const PI = 3.14
console.log(PI)  //3.14
```

2. 객체 선언
```js
const percon = {
  name : 'Park',
  age : 30
}
person.age = 29
console.log(person)  //{ name: 'John', age: 31 }
```

3. 배열 선언
```js
const numbers = [1,2,3]
numbers.push(4)
console.log(numbers)  //[1,2,3,4]
```
4. 함수 선언
```js
const greet = function() {
  console.log('Hello World')
}
greet()
```
5. 화살표 함수 선언
```js
const add = (a,b) => a + b
console.log(add(2, 4))     // 6
```
6. 객체 속성 변경
```js
const student = { name : 'Park'}
strudent.name = 'Lee'
console.log(student)     // Lee
```
7.  배열 내 요소 변경
```js
const colors = ['red', 'green', 'blue']
colors[1] = 'yellow'
console.log(colors)    // [ 'red', 'yellow', 'blue' ]
```
8. for-of 루프에서의 사용
```js
const fruits = ['apple', 'banana', 'cherry']
for(const fruit of fruits) {
  console.log(fruit)
}
```
9. 모듈 수준의 상수
```js
const CONFIG = {
  apiKey : 'ABC123',
  apiUrl : 'https://api.example.com'
}
console.log(CONFIG)
```
10. 함수 인자로서의 사용
```js
const logDetails = (name, age) => {
  console.log(`${name} is ${age} years old`)
}
logDetails('Park', 29)
```





































