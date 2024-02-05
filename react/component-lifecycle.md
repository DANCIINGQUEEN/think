# 컴포넌트의 생명주기
- 마운팅 => 업데이트 => 언마운팅


1. Mounting
   - 컴포넌트가 생성되어 DOM에 삽입되는 단계
   - 주요 메서드 :
     - `constructor()` : 컴포넌트의 생성자 메서드로, 컴포넌트가 생성될 때 한번 호출
     - `static getDerivedStateFromProps()` ; 컴포넌트가 생성될 때 컴포넌트가 받는 props가 변경될 때 호출
     - `render()` : 컴포넌트를 렌더링하는 메서드, UI 반환
     - `componentDidMount()` : 컴포넌트가 마운트된 후에 호출, 여기서 API호출, 이벤트 리스너 설정 등의 작업 수행
2. Updating
   - 컴포넌트의 props 또는 state가 변경될 때 발생
   - 주요 메서드 :
     - `static getDerivedStateFropProps()` : 컴포넌트가 업데이트 될 때 호출
     - `shouldComponentUpdate()` : 컴포넌트가 업데이트 되어야 할지 여부 결정. 성능 최적화에 사용
     - `render()` : 컴포넌트의 UI를 다시 렌더링
     - `getSnapshotBeforeUpdate()` : 업데이트가 일어나기 직전의 DOM 상태 캡쳐
     - `componentDidUpdate()` : 컴포넌트 업데이트 후 호출, 여기서 추가 업데이트 로직을 수행 할 수 있음
3. Unmounting
   - 컴포넌트가 DOM에서 제거되는 단계
   - 주요 메서드 :
     - `componentWillUnmount()` : 컴포넌트가 언마운트되기 전에 호출. 여기서 클린업 작업을 수행
    


## Hooks을 사용하는 함수형 컴포넌트에서는 훅을 사용하여 생명주기를 관리할 수 있음
- `useState` : 컴포넌트의 상태를 정의하고 관리
- `useEffect` : side effect를 실행
- `useContext` : 컨텍스트를 통해 전역 상태나 설정을 컴포넌트에 전달
- `useReducer` : 복잡한 상태 로직을 관리할 때 `useState`의 대안으로 사용됨
- `useMemo`, `useCallback` : 컴포넌트의 성능 최적화를 위해 계산된 값과 함수를 메모이제이션함
