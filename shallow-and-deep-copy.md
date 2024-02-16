# Shallow Copy (얕은 복사)
- 얕은 복사는 객체의 최상위 수준의 값만 복사함
- 만약 객체가 다른 객체를 참조하고 있다면, 참조 값만 복사되어 두 객체가 내부저긍로 같은 객체를 참조하게됨
- 내부 객체가 변경될 때 원본과 복사본 모두에 영향을 줄 수 있음

```js
const original = {a:1, b:{c:2}}
const shallowCopy = { ...original }
console.log(shallowCopy.b === original.b)  //true, 내부 객체가 동일한 참조를 가짐
```
```js
//배열의 얕은 복사
const originalArray = [1,2,3,4]
const shallowCopiedArray = [...originalArray]
shallowCopiedArray.push(5)
console.log(originalArray)  // [1,2,3,4]
console.log(shallowCopiedArray)  // [1,2,3,4,5]
```
```js
//객체의 얕은 복사
const originalObject = {a:1, b:2}
const shallowCopiedObject = { ...originalObject }
shallowCopiedObject.a = 3
console.log(originalObject)  // {a:1, b:2}
console.log(shallowCopiedObject)  // {a:3, b:2}
```

# Deep Copy (깊은 복사)
- 깊은 복사는 객체와 그 객체가 참조하는 모든 객체들까지 재귀적으로 복사함
- 이로 인해 원본 객체와 완전히 독립적인 복사본이 만들어짐
- 내부 객체들까지 모두 새로운 복사본이 생성되어, 원본 객체의 변경이 복사본에 영향을 주지 않음
```js
const original = {a:1, b:{c:2}}
const deepCopy = JSON.parse(JSON.stringify(original))
console.log(deepCopy.b === original.b)  // false, 내부 객체가 서로 다른 참조를 가짐
```
```js
//재귀를 이용한 객체의 깊은 복사
function deepCopy(obj){
  if(typeof obj !== 'object' || obj === null) {
    return obj
  }
  let copy = Array.isArray(obj) ? [] : {}
  for (let key in obj) {
    const value = obj[key]
    copy[key] = deepCopy(value)
  }
  return copy
}
const originalObject = {a:1, b:{c:2, d:[3,4]}}
const deepCopiedObject = deepCopy(originalObject)
deepCopiedObject.b.d.push(5)
console.log(originalObject)    // {a:1, b:{c:2, d:[3,4]}}
console.log(deepCopiedObject)  // {a:1, b:{c:2, d:[3,4,5]}}
```
위 코드의 문제와 한계점
1. 원시 값과 특별한 객체 처리
  - 위 코드는 객체를 복사하는 데에만 초점을 맞추고 있어 원시 값과 특별한 객체(예: 함수, Map, Set 등)에 대한 처리를 고려하지 않음.
2. 순환 참조 처리
  - 순환 참조가 있는 경우 무한 루프에 빠질 수 있음.
  - 예 : 객체 A가 객체 B를 참조, 객체 B가 다시 객체 A를 참조하는 경우
3. 프로토타입 처리
  - 원본 객체에 프로토타입이 있는 경우, 이를 고려하여 복사해야됨
  - 위 코드는 프로토타입을 고려하지 않고 단순히 객체의 속성만을 복사함
4. 속도
  - 큰 깊이를 갖는 중첩된 객체의 경우 재귀적으로 모든 속성을 순회하며 복사하기 때문에 성능에 영향을 줄 수 있음

## immer의 produce함수 사용하기
- `produce`함수는 불변성을 유지하면서 JavaScript 객체나 배열을 업데이트함
  - `produce`함수의 인자
    - 첫번째 인자 (`baseState`) : 이 인자는 변경하고자 하는 원본 객체나 배열 Immer는 이 원본 데이터를 "드래프트 상태"로 변환하여 두번째 인자로 전달되는 함수에 제공
    - 두번째 인자 (`producer`함수) : 이 함수는 드래프트 상태를 인자로 받아 이 드래프트 상태를 직접 변경함으로써 원하는 상태 업데이트를 수행할 수 있음
  - `produce`함수의 기능
    - 불변성 유지 : 원본 객체를 직접 수정하지 않고, 변경사항을 적용한 새로운 객체를 생성하여 반환
    - 드래프트 상태 변경 : 함수의 두번째 인자로 전달된 수정 함수 내에서는 드래프트 상태를 마치 가변 객체처럼 자유롭게 변경할 수 있음
    - 성능 최적화 : 변경이 발생한 부분만을 복사하고, 나머지 부분은 원본 객체와 공유

```js
let { produce } = require('immer')
const originalObject = {
  name : "Park",
  age : 29,
  address : {
    street : "1234",
    city : "Seoul",
    coordinates : {
      lat : 123.123,
      lng : 234.234
    }
  },
  hobbies : ["walking", "baking", "reading"]
}
//깊은 복사본 생성
const deepCopiedObject = produce(originalObject, draft => {
  //새로운 객체 복사본에 변경사항 적용
  //만약 변경사항을 적용하지 않는다면 원본객체를 수정할수없음
  draft.name = "Lee"
  draft.hobbies.push("swimming")
})

console.log(originalObject) 
console.log(deepCopiedObject) 
```









