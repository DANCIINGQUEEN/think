# OOP (Object-Oriented Programming)
1. 클래스와 객체
   - OOP에서는 class를 정의하고 이를 기반으로 object를 생성
   - 객체는 속성(멤버 변수)과 메소드(함수)를 가질 수 있음
2. 상속
   - 클래스 간에 상속을 통해 코드를 재사용할 수 있음
   - 부모 클래스에서 정의된 속성과 메서드를 하위 클래스에서 사용할 수 있음
3. 캡슐화
   - 객체 내부의 상태를 숨기고, 외부에서 접근할 수 있는 메소드를 통해 상호작용하는 개념
4. 다형성
   - 다양한 객체가 동일한 인터페이스를 공유하면서 각 객체가 특정한 방식으로 동작할 수 있도록 하는 개념
## 한계점
   - 복잡성 관리 : 상속, 다형성, 캡슐화 등의 개념을 사용하여 코드를 구성하는데, 이로 인해 복잡성이 증가할 수 있음. 상속의 남용은 코드의 가독성을 떨어뜨릴 수 있음
   - 상태 관리 : 객체는 상태를 가지고 있으며, 이 상태를 변경하면서 부작용이 발생할 수 있음
   - 동시성 : OOP는 상태를 공유하는 객체들 사이의 상호작용에 의지함. 따라서 동시성 문제를 다루기 어려울 수 있음

```js
class Person {
  constructor(name, age) {
    this.name = name
    this.age = age
  }
  introduce() {
    console.log(`안녕하세요, 제 이름은 ${this.name}이고, ${this.age}살입니다`)
  }
}
//class inheritance
class Student extends Person {
  constructor(name, age, grade) {
    super(name, age)
    this.grade = grade
  }
  showGrade() {
    console.log(`${this.name}은 ${this.grade}학년입니다.`)
  }
}
//Encapsulation information hiding
class BankAccount {
  constructor(balance) {
    let _balance = balance  //private variable

    this.getBalance = function() {
      return _balance
    }

    this.deposit = function(amount) {
      _balance += amount
    }

    this.withdraw = function(amount) {
      if (_balance >= amount) {
        _balance -= amount
        console.log(`${amount}원이 출금됨`)
      } else {
        console.log("잔액이 부족함")
      }
    }
  }
}
//polymorphism : 다형성, 여러 객체가 동일한 인터페이스를 공유하면서 각자의 동작을 수행
let people = [
  new Person("Park", 29),
  new Student("Lee", 20, 1)
]

people.forEach(person => {
  person.introduce()
  if(person instanceof Student) {
    person.showGrade()
  }
})

let account = new BankAccount(1000)
console.log("current:", account.getBalance())  //1000
account.deposit(500)
console.log("current:", account.getBalance())  //1500
account.withdraw(2000)  //잔액이 부족함
account.withdraw(1000)  //1000원이 출금됨
console.log("current:", account.getBalance())  //500
```

# FP (Functional Programming)
1. 순수 함수
   - 함수형 프로그래밍에서는 순수 함수를 중심으로 프로그래밍함
   - 동일한 입력에 대해 항상 동일한 출력을 반환, 부작용이 없어야함
2. 불변서성
   - 데이터는 불변(immutable)해야 하며, 새로운 데이터를 생성하는 방식으로 상태를 변경
3. 고차 함수
   - 함수를 인자로 받거나 함수를 반환할 수 있음
   - 함수를 조합하고 추상화하여 코드를 작성하는 것이 중요
4. 재귀
   - 반복 대신 재귀를 사용하여 문제를 해결하는 경향이 있음
## 한계점
   - 외부 상태에 의존하는 경우 : 외부 상태와의 상호작용이 필요한 경우 부수 효과를 최소화하고 불변성을 유지하는것이 어려움
   - 성능 문제 : 예 : 재귀적인 방식으로 구현한 피보나치 수열은 중복 계산이 발생하면서 성능이 저하될 수 있음

```js
//pure function : 동일한 입력에 대해 항상 동일한 출력을 반환하고 부작용이 없음
function add(a, b) {
  return a + b
}

//immutable  : 데이터는 불변해야됨
const numbers = [1,2,3,4,5]
const doubleNumbers = numbers.map(num => num*2)

//higher order function : 함수를 인자로 받거나 함수를 반환할 수 있음
function higherOrderFunction(func, x, y){
  return func(x, y)
}
function multiply(x, y) {
  return x*y
}

console.log(higherOrderFunction(multiply, 3, 4))  //12

//recursion : 반복 대신 재귀를 사용하여 문제를 해결
function factorial(n) {
  if( n=== 0 || n === 1) {
    return 1
  } else {
    return n*factorial(n-1)
  }
}
console.log(factorial(5))  //5! = 120
```
















