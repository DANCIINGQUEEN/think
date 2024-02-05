closure : 폐쇄, 종료, 종결시키다

클로저 예시
```js
function getClosure () {
  var freeVar = 'independent'
  return function () {
    return freeVar
  }
}
var closure = getClosure()
console.log(closure()) // 'independent'
```
클로저는 함수가 선언될 때의 환경을 기억하는 함수.

1. 'getClosure'함수 정의 및 반환
   getClosure라는 이름의 함수 내부에서는 freeVar라는 변수가 선언.
   freeVar는 'independent'라는 문자열로 초기화
   이 변수는 getClosure 함수의 로컬 변수
   getClosure함수는 다시 한번 함수를 반환
   이 내부 함수는 외부 함수인 getClosure의 변수 freeVar에 접근하여 이 값을 반환하는 역할
   이 내부 함수가 바로 클로저.

 2. 클로저의 특징
    클로저는 자신이 생성될 때의 환경을 '기억'
    여기서 말하는 환경은 클로저가 선언될 때 접근 할 수 있었던 변수들의 집합
    따라서 getClosure함수의 실행 컨텍스트가 종료된 후에도 반환된 클로저는 freeVar에 접근할 수 있음
    이는 javaScript의 스코프 체인 때문에 가능한 것
    함수가 실행될 때, 해당 함수는 자신의 스코르(자신의 변수와, 부모 스코프의 변수에 접근할 수 있는 권한)을 생성,
    클로저는 이 스코프 체인을 통해 자신이 선언될 당신의 환경에 계속해서 접근할 수 있음

  3. 코드 실행 과정
     var closure = getClosure() 코드를 실행하면 getClosure함수가 호출
     이 함수는 내부에서 freeVar변수 선언하고 이 변수를 사용하는 클로저(익명 함수)를 반환
     반환된 클로저는 closure변수에 저장, 이 시점에서 getClosure함수의 실행 컨텍스트는 종료되어도,
     클로저는 freeVar변수의 값에 접근할 수 있는 '기억'을 유지
     마지막으로 console.log(closure()) 코드를 실행하면, closure변수에 저장된 클로저 함수가 호출
     이 클로저는 freeVar변수의 값을 반혼하고, 이 값은 콘솔에 independent라고 출력.

  4. 마무리
     이러한 클로저의 특성 덕분에, JavaScript에서는 비동기 처리, 데이터 캡슐화,
     고차 함수에서의 상태 유지 등 다양한 프로그래밍 패턴을 구현할 수 있음
     클로저는 함수형 프로그래밍에서 특히 유용한 개념으로, 데이터를 안전하게 은닉하고,
     특정 함수에 지속적인 상태를 부여하는 데 사용



```js
var i;
for(i=0; i<10; i++){
    setTimeout(function(){
        console.log(i);
    }, 100);
}
```

### 결과 
  - 10을 10번 출력
### 이유 
  -  var키워드로 선언된 i는 함수 스코프를 가지므로 setTimeout의 콜백 함수가 실행될 때 for반복문이 이미 종료되어 i의 값이 10이 된 상태.
  -  모든 setTimeout콜백에서 참조하는 i는 같은 변수이며, 그 값은 반복문이 종료된 후의 최종 값인 10
  

```js
var i;
for(i=0; i<10; i++){
    (function(j){
        setTimeout(function(){
            console.log(j);
        }, 1000);
    })(i);
}
```

### 결과 
  - 0부터 9까지의 숫자를 각각 출력
### 이유 
  -  즉시 실행 함수 표현식(IIFE, Immediately Invoked Function Expression)을 사용하여 각 반복마다 i의 현재 값을 j라는 새로운 변수에 복사.
  -  j는 IIFE의 매개변수로, IIFE가 실행될 때마다 새로운 스코프를 생성하므로, 각 setTimeout콜백은 자신만의 j값을 가진 독립적인 스코프에서 실행.
  -  각 콜백은 반복문의 각 단계에 해당하는 0부터 0까지의 i값을 j를 통해 '기억'하고 예정된 시간(1000ms) 후에 해당 값 출력


# 클로저 사용의 이점

  ## 상태 캡슐화 
  -  클로저를 사용하면 특정 데이터(상태)를 함수 내부에 안전하게 숨길 수 있음
  -  선택적으로 이 상태를 조작할 수 있는 함수만을 외부에 노출 할 수 있음
    -  객체 지향 프로그래밍에서 비공개(private) 맴버 변수와 유사한 효과 제공
  ## 모듈성
  -  코드를 모듈화하여 각 모듈이 자신만의 비공개 상태를 가질 수 있게 함
    -  전역 변수의 사용을 줄이고 코드의 관리를 용이하게 함

# 4가지 클로저 사용 사례

## 이벤트 핸들러
```js
function setupButton(buttonId, message) {
  document.getElementById(buttonId).addEventListener('click', function() {
      alert(message)
  })
}
setupButton('myButton', '버튼이 클릭됨')
```
- 클로저는 이벤트 핸들러 내에서 특정 데이터를 기억하기 하는 데 사용될 수 있음
- 생성 시점의 환경을 '기억'하고 이후에 발생하는 이벤트에 따라 해당 데이터를 사용할 수 있음
- 위의 코드에서 setupButton함수는 클로저를 사용하여 각 버튼의 ID와 메시지를 기억함
- 이벤트리스너는 클로저를 형성하여 message변수의 값을 기억하고, 버튼이 클릭될 때마다 해당 메시지를 표시


## 비동기 처리

```js
function fetchData(url, callback) {
  fetch(url)
    .then(res => res.json())
    .then(data => callback(data))
    .catch(e => console.log('err', e))
}
function processResult(result) {
  console.log('데이터 처리', result)
}
fetchData('https://api.example.com/data', processResult)
```
- 클로저는 비동기 작업을 수행할 때 결과를 처리하는 콜백 함수 내부에서 상태를 유지하는 데 사용될 수 있음
- 각 비동기 작업이 완료될 때마다 해당 작업의 컨텍스트에 접근할 수 있음
- 위 코드에서 fetchData함수는 비동기적으로 데이터를 가져오고, 결과를 처리하는 콜백함수에 전달함
- 클로저는 비동기 호출과 결과 처리 사이의 연결 고리 역할을 함


## 데이터 캡슐화
```js
function createCounter(){
  let count = 0
  return {
    increment : function() {
      count++
      console.log(count)
    },
    decrement : function() {
      count--
      console.log(count)
    },
    getCount : function() {
      return count
    }
  }
}
const counter = createCounter();
counter.increment(); // 1
counter.decrement(); // 0
```
- 클로저는 데이터 캡슐화의 정보 은닉에 사용될 수 있음
- 객체의 특정 데이터에 대한 직접적인 접근을 제한하고, 메소드를 통해서만 데이터를 조작할 수 있도록 함
- 위 코드에서 createCounter함수는 count변수를 내부에 캡슐화하고, 이 변수를 조작하는 메소드들을 제공.
- 이 메소드들은 클로저를 형성하여 count변수에 접근할 수 있음

## 고차 함수에서의 콜백 관리
```js
function filerArray(elements, criteria) {
  return elements.filter(criteria)
}
const numbers = [1,2,3,4,5]
const evenNumber = filterArray(numbers, function(number){
  return number%2===0
}
console.log(evenNumber)
```
- 고차 함수는 다른 함수를 인자로 받거나 함수를 결과로 반환하는 함수
- 클로저는 고차 함수가 콜백 함수를 관리하는 데 사용될 수 있음
- 위 코드에서 filterArray 함수는 배열과 조건을 만족하는 요소를 필터링하는 콜백 함수를 인자로 받음
- 콜백 함수는 클로저를 형성하여 criteriaㅎ마수의 로직에 따라 배열의 각 요소를 평가함



데이터 캡슐화는 객체 지향 프로그래밍의 핵심 원칙 중 하나로, 클래스를 이용해서도 구현 할 수 있음
클로저와 클래스 모두 데이터 캡슐화를 구현할 수 있지만, 그 방식과 사용되는 컨텍스트에 차이가 있음

### 클래스를 이용한 데이터 캡슐화
```js
class Conter {
  #counter = 0
  increment() {
    this.#counter++
    console.log(this.#count)
  }
  decrement() {
    this.#count--
    console.log(this.#count)
  }
}
const counter = new Counter()
counter.increment()  // 1
counter.decrement()  // 0
```
- 클래스를 이용한 데이터 캡슐화는 객체 지향 프로그래밍의 전형적인 접근 방식.
- 클래스 내부에 private 필드나 메소드를 선언하여 데이터를 캡슐화하고, public 메소드를 통해 외부에서 접근할 수 있는 인터페이스 제공
- 위 코드에서 #count는 private필드로, 클래스 외부에서 직접 접근할 수 없음
- increment와 derement메소드는 public 인터페이스로 객체의 상태를 안전하게 조작할 수 있음

### 클로저와 클래스의 캡술화 차이점
  - 구현 방식
        - 클래스를 이용한 캡술화는 객체 지향의 명시적인 구문과 구조를 사용
        - 클러조를 이용한 캡슐화는 함수의 스코프를 이용해 데이터를 숨김
    - 사용 패러다임
        - 클래스는 객체 지향 프로그래밍의 전형적인 특성을 따름
        - 클로저는 함수형 프로그래밍의 특정 반영
    - 접근성 제어
        - 클래스에서는 private, protected, public과 같은 접근 제어자를 통해 데이터와 메소드의 접근성을 명시적으로 제어할 수 있음
        - 클로저는 이러한 제어자가 없지만, 함수 스코프를 이용하여 데이터를 숨시는 효과를 낼 수 있음
