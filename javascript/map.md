# Map
ECMAScript6(ES6)부터 추가된 자료구조로, 키-값 쌍을 저장하는 컬렉션

1. 키-값 쌍
   - 키와 값을 하나의 쌍으로 저장. 이를 통해 각 키에 해당하는 값을 쉽게 찾을 수 있음
2. 키의 고유성
   - `Map`은 키의 중복을 허용하지 않음. 즉, 동일한 키가 여러 번 등장할 수 없음. 각 키는 유일해야됨
3. 객체를 키로 사용 가능
   - 객체를 키로 하는 해시맵을 만들 수 있게 해주며, 객체의 메모리 주소를 기준으로 식별
4. 순서 보존
    - 요소들의 삽입 순서를 유지함. 따라서 요소를 추가한 순서대로 반복문 등을 통해 접근 가능
5. 크기 확인
   - 객체의 크기(키-값 쌍의 수)는 `size` 프로퍼티를 통해 확인할 수 있음
6. 반복 가능한 객체
   - `Map`은 반복 가능한(iterable) 객체이므로, `for...of`루프나 `forEach` 메서드 등을 사용하여 요소를 순회할 수 있음
7. 참조 유지
   - 요소들을 추가한 순서대로 유지하기 때문에 순서가 중요한 상황에서 유용
8. 효율적이 검색 및 삭제
   - 객체의 속성을 키로 사용하는 것보다 `Map`이 더 빠르고 요소를 검색하거나 삭제할 수 있음
  
```js
let myMap = new Map()

myMap.set('name', 'Park')
myMap.set('age', 29)
myMap.set('id', 'User ID 1')

console.log(myMap.get('name'))   //Park
console.log(myMap.size)   //3

myMap.delete('age')
console.log(myMap.has('age'))   //false

for (let [key, value] of myMap) {
  console.log(`${key} => ${value}`)    //id => User ID 1
}
```
