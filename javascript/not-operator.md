# ~
`~`는 비트 NOT 연산자. 이 연산자는 피연산자의 비트를 뒤집음. 각 비트의 상태를 반전시킴

1. 비트 연산
   - 정수 값을 32비트 이진수로 나타낸 후 각 비트를 반전함
2. 인덱스 계산
   - 배열의 인덱스를 계산할 때 유용하게 사용될 수 있음. 예 : `~i`는 `-i-1`의 값을 얻는데 사용됨, `~0`은 `-1`
3. 비트 마스킹
   - 특정 비트를 끄거나 켤 때 사용될 수 있음. 예 : `value & ~mask` 는 `mask` 비트를 끄고 `value`를 유지
4. 정수 변환
   - `~~`는 두번 사용하여 소수 부분을 제거하고 정수 부분만 남김
  


```js
let num1 = 5
let bitwiseNot1 = ~num1 // -6

let num2 = 3
let bitwiseNot2 = ~num2 // -4

let zero = 0
let bitwiseNot3 = ~zero // -1

let value = 10
let mask = 2
let result = value & ~mask // 8
// value   ==> 00001010
// mask    ==> 00000010
//~mask    ==> 11111101
//value & ~mask   => 00001010 (10) & 11111101 (-3) = 00001000 (8)


let floatNum = 3.7
let integerPart = ~~floatNum // 3
```
