# iterable
- 반복 가능한 객체
- 즉, 그 객체의 요소들을 하나씩 차례대로 접근할 수 있는 구조를 가진 객체
- `for...of` 루프와 같은 반복문을 통해 순회할 수 있으며, 이 과정에서 객체 내부의 각 요소들을 순차적으로 처리할 수 있음

```js
let numbers = [1,2,3,4,5]
for( let number of numbers) {
  console.log(number)
}
```

## iterable 사용의 이점
- 컬렉션의 요소를 쉽고 명확하게 순회할 수 있음
- 다양한 유형의 데이터 구조를 효율적으로 처리할 수 있음
- 전개 연산자, 구조 분해 할당 같은 다른 기능과 함께 사용될 수 있음
