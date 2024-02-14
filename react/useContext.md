# useContext
- context API를 사용할 수 있게 해주는 hook
- context API는 react 컴포넌트 트리 안에서 전역저긍로 데이터를 공유할 수 잇는 방법을 제공함
- 애플리케이션의 테마, 언어 설정, 사용자 인증 정보 등과 같이 여러 컴포넌트에서 접근해야 하는 데이터를 관리할 때 유용
- `useContext`를 사용하면, 컴포넌트가 직접적으로 데이터를 전달받지 않고도 해당 데이터에 접근할 수 있음


## 사용법 
### 1. 컨텍스트 생성
- `React.createContext` 를 호출하여 컨텍스트를 생성. 이 함수는 `Provider`와 `Consumer`컴포넌트를 포함하는 객체를 반환
```js
import React from 'react'
const Mycontext = React.createContext(initialValue)
```
### 2. Provider를 사용한 값 제공
- 컨텍스트 `Provider`를 사용하여 컨텍스트 값을 하위 컴포넌트에게 제공함. `Provider`는 `value` prop을 통해 공유하고자 하는 데이터를 받음
```js
<MyContext.Provider value={/* 공유하고자 하는 값*/}>
  {/*여기에 포함된 컴포넌트들은 MyContext의 값을 접근할 수 있음*/}
</MyContext.Provider>
```

### 3. useContext 사용한 값 접근
- 함수 컴포넌트 내에서 `useContext` Hook을 사용하여 `Provider`를 통해 제공된 값을 접근할 수 있음
```js
import React, { useContext } from 'react'
function MyComponent() {
  const contextValue = useContext(MyContext)
}
```

## useContext의 장점
- Prop Drilling 회피
  - 컨텍스트를 사용하면 중간 단계의 컴포넌트를 거치지 않고도 깊은 단계의 컴포넌트에게 데이터를 직접 전달할 수 있음
  - 컴포넌트 트리에서 데이터를 효율적으로 관리할 수 있게 해주며, 코드의 복잡성을 줄여줌
- 코드의 재사용성 향상
  - 공통 데이터를 사용하는 컴포넌트들이 동일한 컨텍스트를 공유함으로써, 컴포넌트 간의 결합도를 낮추고 재사용성을 향상시킬 수 있음
- 성능 최적화
  - `useContext`를 사용하면 필요한 컴포넌트만 컨텍스트의 변화를 감지하고 업데이트될 수 있음
  - 불필요한 렌더링을 방지하고 애플리케이션의 성능을 최적화함
