# function 키워드로 선언된 함수의 this
- function으로 선언된 함수에서 this의 값은 함수가 호출되는 컨텍스트에 따라 '동적'으로 결정
- 실행 시점에 this가 누구인지 결정된다는 뜻

1. 전역 컨텍스트에서 function으로 선언된 함수를 호출하면, this는 전역 객체를 가리킴
2. 메소드로서 호출되면 this는 메소드를 호출한 객체를 가리킴
3. 생성자 함수로서 호출되면 새로 생성된 객체를 this로 가리킴
4. call, apply, bind 메소드를 이용한 호출에서는 명시적으로 지정된 객체를  this로 가리킴
 
  ```js
  function show() {
    console.log(this)
  }
  const obj = {
    method : function() {
      console.log(this)
      }
  }
  show()    //전역 객체 : Window {0: Window, 1: Window, 2: Window, window: Window, self: Window, document: document, name: '', location: Location, …}
  obj.method()    // {method: ƒ}
  new show()     //show {}
  show.call(obj)    // {method: ƒ}
  ```

```js
function Person(name) {
 this.name = name
 this.sayHello = function() {
  console.log(`Hello, my name is ${this.name}`)
 }
}
const john = new Person('John')
john.sayHello()  // Hello, my name is John
const sayHello = john.sayHello
sayHello()  //Hello, my name is undefined (브라우저에서는 window.name)
```

# 화살표 함수의 this
- 화살표 함수에서 this는 '정적'으로 결정
- 화살표 함수는 자신이 선언된 렉시컬 환경의 this를 상속받음(자신을 포함하고 있는 외부 함수의 this값을 상속받음)
- 화살표 함수가 정의될 때 this가 무엇인지에 따라 결정되며, 실행 시점에서는 변경되지 않음


1. 화살표 함수는 자신을 포함하고 있는 외부 함수의 this값을 사용
2. 만약 화살표 함수가 전역 범위에서 정의된 경우, this는 전역 객체를 가리킴
3. 화살표 함수는 bind, call, apply 메소드를 통해 this를 변경할 수 없음

```js
const obj = {
  method : function() {
    const arrowFunc = () => {
      console.log(this)
    }
    arrowFunc()
}
obj.method()  // {method: ƒ}
const globalArrowFunc =() => console.log(this)
globalArrowFunc()  //전역 객체   Window {0: Window, 1: Window, 2: Window, window: Window, self: Window, document: document, name: '', location: Location, …}
```
```js
function Person(name) {
 this.name = name
 this.sayHello = () => {
  console.log(`Hello, my name is ${this.name})
 }
}
const john = new Person("John")
john.sayHello() // Hello, my name is John
const sayHello = john.sayHello
sayHello()  //Hello, my name is John
```

## 결론
- function으로 선언된 함수와 화살표 함수의 this 처리 방식의 차이는 주로 this 바인딩의 '동적'인 결정 대 '정적' 결정에 기반
- function 함수가 다양한 상황에서 유연하게 this를 다룰 수 있도록 함
- 화살표 함수는 렉시컬 스코프를 기반으로 this를 예측 가능하기 만듦
- 따라서 화살표 함수는 메소드나 생성자 함수보다는 콜백 함수나 클로저 내부 함수로 사용될 때 더 적함합수도..?


```html
<button id='button'>click me</button>
```
```js
//function키워드 사용
document.getElementById('button').addEventListener('click', function(){
 console.log(this) //이 경우 this는 button요소를 가리킴
}

//화살표 함수 사용
document.getElementById('button').addEventListener('click', ()=>{
 console.log(this)  // 화살표 함수 외부의 this를 상속받음
}
```
- 화살표 함수는 이벤트 핸들러 내에서 this를 핵당 요소로 바인딩하는 대신, 외부 스코프의 this를 사용함
- 따라서 화살표 함수는 이벤트 핸들러에서 DOM 요소를 직접 참조하기 위한 this를 사용할 때 주의해야함
- 반면, function 키워드 함수는 이벤트 리스너가 추가된 요소를 this로 자동 바인딩 함
- 따라서 이벤트 대상 요소에 접근하려면 function키워드 함수가 더 적합할수도..
