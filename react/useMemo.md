# useMemo
- 메모이제이션된 값을 반환하는 데 사용
- 성능 최적화를 위해 주로 사용되며, 비싼 계산 비용이 드는 연산의 결과를 메모리에 저장해두고, 동일한 입력에 대해서 재계산 없이 저장된 값을 사용

## Memoization
  - `useMemo`는 계산된 값을 메모리에 저장함. 이전에 계산된 값을 캐시하는 매커니즘으로, 동일한 계산을 반복 수행하지 않도록 함
  - 메모이제이션된 값은 해당 값이 의존하는 데이터나 변수가 변경되지 않는 한 유지됨.
## Dependency Array
  - `useMemo`의 두 번째 인자로 전달되는 배열은 의존성 배열이라고 함
  - 의존성 배열은 메모이제이션된 값이 의존하는 변수나 데이터를 나타내며, 이 값들이 변경될 때만 메모이제이션된 값이 다시 계산
  - 의존성 배열은 `useMemo`가 어떤 조건에서 메모이제이션된 값이 다시 계산되어야 하는지 결정하는데 중요한 역할을 함
## 성능 최적화 
  - `useMemo`를 사용하면 불필요한 렌더링과 계산을 방지하여 애플리케이션의 성능을 향상시킴


### 간단한 예시
```js
import React, { useMemo, useState } from 'react'

function calculationComplexValue(num) {
  //복잡한 계산을 수행하는 함수
  console.log('계산중..')
  return num*2  //예시를 위한 간단한 계산
}

functinon MyComponent() {
  const [num, setNum] = useState(0)
  const [otherState, setOtherState] = useState(false)

  const doubleValue = useMemo(() => calculateComplexValue(num), [num])
  return (
    <div>
      <p>Value : {doubleValue}</p>
      <button onClick={() => setNum(num + 1)}>Increase</button>
      <button onClick={() => setOtherState(!otherState)}>Toggle State</button>
    </div>
  );
}
```

## useMemo 사용시 주의사항
  - 필요한 경우에만 사용 : 모든 값에 `useMemo`를 사용하는 것은 오히여 성능에 부정적인 영향을 미침. 비싼 계산이나 렌더링 최적화가 필요한 경우에만 사용
  - 참조 동일성 유지 : 객체나 배열과 같은 복잡한 타입을 반환할 때, `useMemo` 는 참조 동일성을 유지함. 이는 불필요한 자식 컴포넌트의 리렌더링을 방지할 수 있음





## useMemo 사용 예시

### 1. 메모이제이션된 객체
```js
import React, { useMemo, useState } from 'react'
function App() {
  const [count, setCount] = useStaet(0)
  const memoizedObject = useMemo(() => ({ count }), [count])

  return (
    <div>
      <button onClick={() => setCount(count + 1)}>Increment</button>
      <div>{JSON.stringify(memoizedObject)}</div>
    </div>
  )
}
```

### 2. 필터링된 목록
```js
import React, { useMemo, useState } from 'react'

const userList = [{ name : 'Park' }, { name : 'Lee' }, { name : 'Hong' }]

function App () {
  const [filter, setFilter] = useState('')
  const filteredList = useMemo(() => userList.filter((user) => user.mame.includes(filter)), [filter])
  
  return (
     <div>
        <input
          type="text"
          value={filter}
          onChange={(e) => setFilter(e.target.value)}
        />
        <ul>
          {filteredList.map((user, index) => (
            <li key={index}>{user.name}</li>
          ))}
        </ul>
      </div>
    )
}
```

### 3. 복잡한 데이터 변환 
```js
import React, { useMemo, useState } from 'react'
function processData(data) {
  //복잡한 데이터 변환 로직
  return data.map((item) => item*2)
}

function App() {
  const [data, setData] = useState([1,2,3,4,5])
  const processData = useMemo(() => processDatadata(data), [data])
  return (
     <div>
      {processedData.map((item, index) => (
        <div key={index}>{item}</div>
      ))}
    </div>
  )
}
```

### 4. 조건부 렌더링 최적화
```js
import React, { useMemo, useState } from 'react'
functino App() {
  const [count, setCount] = useState(0)
  const [isEven, setIsEven] = useState(true)

  const evenStatus = useMemo(() => {
    return isEven ? 'Even' : 'Odd'
  }, [isEven])

  return (
    <div>
      <button onClick={() => setCount(count + 1)}>Increment</button>
      <button onClick={() => setIsEven(!isEven)}>Toggle Even/Odd</button>
      <div>Count: {count}, Number is {evenStatus}</div>
    </div>
  )
}
```
















