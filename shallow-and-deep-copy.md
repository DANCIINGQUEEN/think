# Shallow Copy (얕은 복사)
- 얕은 복사는 객체의 최상위 수준의 값만 복사함
- 만약 객체가 다른 객체를 참조하고 있다면, 참조 값만 복사되어 두 객체가 내부저긍로 같은 객체를 참조하게됨
- 내부 객체가 변경될 때 원본과 복사본 모두에 영향을 줄 수 있음

```js
const original = {a:1, b:{c:2}}
const shallowCopy = { ...original }
console.log(shallowCopy.b === original.b)  //true, 내부 객체가 동일한 참조를 가짐
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
