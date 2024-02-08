# for

1. for...of loop
배열이나 이터러블 객체를 순회할 때 사용
```js
let arr = [1,2,3]
for (let e of arr) {
  console.log(e)
}
```

2. forEach() method
배열의 각 요소에 대해 콜백 함수 실행
```js
let arr = [1,2,3]
arr.forEach(function(e) {
  console.log(e)
})
```

3. map() method
배열의 각 요소에 대해 콜백 함수를 실행하고, 새로운 배열 반환
```js
let arr = [1,2,3]
let newArr = arr.map(function(e) {
  return e * 2
})
```

4. for...in loop
객체의 속성을 순회할 때 사용. 주로 객체에 대한 반복 작업에 사용
```js
let obj = {a:1, b:2, c:3 }
for (let key in obj) {
  console.log(key + ": " + obj[key])
}
```

5. while loop
조건을 만족하는 동안 루프를 실행
```js
let i = 0
while  (i < 5) {
  console.log(i)
  i++
}
```

6. do...while loop
일단 한번은 루프를 실행하고, 그 다음에 조건을 검사하여 계속할지 결정
```js
let i = 0
do {
  console.log(i)
  i++
} while ( i < 5)
