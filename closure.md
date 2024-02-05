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
   getClosure함수는 다시 한 번 함수를 반환
   이 내부 함수는 외부 함수인 getClosure의 변수 freeVar에 접근하여 이 값을 반환하는 역할
   이 내부 함수가 바로 클로저.

 2. 클로저의 특징
    클로저는 자신이 생성될 때의 환경을 '기억'
    여기서 말하는 환경은 클로저가 선언될 때 접근 할 수 있었던 변수들의 집합
    따라서 getClosure함수의 실행 컨텍스트가 종료된 후에도 반환된 클로저는 freeVar에 접근할 수 있음
    이는 javaScript의 스코프 체인 때문에 가능한것
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
     이러한 클로저의 특성 덕분에, JavaScript에서느느 비동기 처리, 데이터 캡슐화,
     고차 함수에서의 상태 유지 등 다양한 프로그래밍 패턴을 구현할 수 있음
     클로저는 함수형 프로그래밍에서 특히 유용한 개념으로, 데이터를 안전하게 은닉하고,
     특정 함수에 지속적인 상태를 부여하는 데 사용
