# 전역 상태 관리 Global State Management


## 1. 데이터의 일관성 유지
- **문제** : 프론트엔드 애플리케이션에서 동일한 데이터를 여러 컴포넌트가 사용하는 경우, 데이터의 일관성을 유지하기 어려울 수 있음
  - 예 : 사용자 정보가 여러 페이지와 컴포넌트에 표시되고, 한 곳에서 사용자 정보가 변경되면 모든 곳에서 일관성 있게 업데이트되어야 함
- **해결** : 전역 상태 관리 시스템을 사용하면, 모든 컴포넌트가 동일한 데이터 소스를 참조하게 됨. 데이터가 변경될 때 중앙 저장소에서 한 번만 업데이트하면, 관련된 모든 컴포넌트에서 이 변경사항을 반영할 수 있음. 이로 인해 데이터의 일관성과 신뢰성이 보장됨
  ```js
  //actions/userActions.js
  export const setUserProfile = (useProfile) => ({
    type : 'SET_USER_PROFILE',
    payload : userProfile
  })

  //reducer/userReducer.js
  const initialState = {
    name : '',
    email : ''
  }

  export const userReducer = (state = initialState, action) => {
    switch (action.type) {
      case : 'SET_USER_PROFILE':
        return {
          ...state,
          ...action.payload,
        },
      default :
        return state
    }
  }
  ```


## 2. 컴포넌트 간 통신 최소화
- **문제** : 컴포넌트 간에 상태를 전달하기 위해서는 props 또는 콜백 함수를 사용하는 등의 복잡한 데이터 흐름을 관리해야 함. 특히, 멀리 떨어진 컴포넌트 간의 데이터 전달은 매우 번거로움
- **해결** : 전역 상태 관리를 사용하면 컴포넌트는 중앙 저장소에서 직접 필요한 상태를 조회하거나 업데이트할 수 있음. 이 방식은 컴포넌트 간의 직접적인 통신 필요성을 제거하여, 애플리케이션의 데이터 흐름을 간소화하고 개발의 복잡성을 줄여줌
  ```js
  // UserProfile.js
  import React from 'react'
  import { useSelector } from 'react-redux'

  const UserProfile = () => {
    const user = useSelector(state => state.user)
    return (
        <div>
            <h1>{user.name}</h1>
            <p>{user.email}</p>
        </div>
      )
  }
  export default UserProfile
  ```


## 3. 재사용성과 유지보수의 용이성
- **문제** : 상태 관리 로직이 여러 컴포넌트에 분산되어 있으면, 같은 로직의 중복이 발생하건, 한 부분의 변경이 다른 여러 부분에 영향을 미칠 수 있음
- **해결** : 전역 상태 관리 시스템을 사용하면, 상태 관리 로직을 중앙에서 관리할 수 있음. 로직의 재사용성을 높이고, 한 곳에서 변경사항을 관리할 수 있게 되어, 전반적인 애플리케이션 유지보수를 용이하게 함


## 4. 성능 최적화
- **문제** : 애플리케이션의 여러 부분에서 같은 데이터를 사용할 때, 데이터라 변경될 때마다 관련된 모든 컴포넌트를 리렌더링해야됨. 이는 성능 저하로 이어질 수 있음
- **해결** : 전역 상태 관리를 통해, 데이터 변경이 필요한 컴포넌트만 선택적으로 리렌더링 할 수 있음. 대부분의 상태 관리 라이브러리는 내부적으로 성능 최적화 기법을 적용하여, 불필요한 리렌더링을 최소화
  ```js
  const user = useSelector(state => state.user)
  ```


## 5. 상태의 예측 가능성 및 디버깅
- **문제** : 애플리케이션의 상태가 여러 곳에 분산되어 있고, 비동기 작업 등 복잡한 상태 변화가 일어날 때, 애플리케이션의 동작을 예측하고 디버깅하기 어려울 수 있음
- **해결** : 전역 상태 관리 시스템은 상태 변화의 추적을 용이하게 함.
  - 예 : Redux는 모든 상태 변화를 액션을 통해 관리하며, 이 액션들의 로그를 쉽게 조회할 수 있도록 함. (Redux DevTools 사용)






















