# Polymorphism 다형성
같은 인터페이스를 사용하여 여러 타입의 객체를 처리하는 능력. 메소드나 연산자 등이 다양한 타입의 객체에 대해 다르게 동작할 수 있는 능력
```js
class Animal {
  constructor(name) {
    this.name = name
  }

  makeSound() {
    console.log('Generic animal sound')
  }
}

class Dog extends Animal {
  makeSound() {
    console.log('Woof! Woof!')
  }
}
class Cat extends Animal {
  makeSound() {
    console.log('Meow')
  }
}
class Bird extends Animal {
  makeSound() {
    console.log('Tweet Tweet')
  }
}

function handleAnimalSound(animal) {
  animal.makeSound()
}
const dog = new Dog('Buddy')
const cat = new Cat('Mya')
const bird = new Bird('sparrow')

handleAnimalSound(dog)
handleAnimalSound(cat)
handleAnimalSound(bird)
```
- `Animal` 클래스를 상속한 `Dob`, `Cat`, `Bird` 클래스들은 각각 `makeSound` 메서드를 오버라이드하여 다르게 동작함
- `handleAnimalSound`함수는 다형성을 활용하여 어떤 종류의 동물 객체든 받아들이고 해당 객체의 `makeSound` 메서드를 호출함
