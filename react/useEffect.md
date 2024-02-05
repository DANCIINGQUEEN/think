# useEffect의 3가지 용도

## 데이터 가져오기, 구독 설정 및 수동 DOM 조작
- 네트워크 요청을 보내 데이터를 가져오거나, 이벤트 리스너를 설정/제거하고, 수동으로 DOM을 조작하는 등의 작업을 할 수 있음
    - 예시 1. 데이터 가져오기 : API에서 데이터를 가져와 상태에 저장
    ```js
      import React, { useState, useEffect } from 'react'
      function FetchData() {
        const [data, setData] = useState([])
    
        usEffect(()=>{
          fetch('https://api.example.com/data')
            .then(res => res.json())
            .then(date => setData(data))
        }, [])  //의존성 배열이 비어 있으므로 커포넌트 마운트 시에만 실행
    
        return (
          <div>
            {data.map(item => (
              <p key={item.id}>{item.title}</p>
            ))}
          </div>
        )
      }
  ```

    - 예시 2. 이벤트 리스너 설정 및 제거 : 브라우저의 리사이즈 이벤트에 리스너를 추가하고 제거함
    ```js
      import React, { useState, useEffect } from 'react'
      function WindowSize() {
        const [size, setSize] = useState(window.innerWidth)
        useEffect(() => {
          function updateSize() {
            setSize(window.innerWidth)
          }
          window.addEventListener('resize', updateSize)
          return () => {
            window.removeEventListener('resize', updateSize)
          }
        }, [])  //의존성 배열이 비어 있으므로 컴포넌트 마운스 시에만 실행
    ```

    - 예시 3. 수동 DOM 조작 : DOM 요소의 타이틀을 업데이트
    ```js
      import React, { useEffect } from 'react'
      function UpdateTitle() {
        useEffect(() => {
          document.title = '새 페이지 타이틀'
          return () => {
            document.title = '이전 페이지 타이들'
          }
        }, [])    //의존성 배열이 비어 있으므로 컴포넌트 마운트 시에만 실행
        return <h1>페이지 타이틀</h1>
      }
    ```

## 의존성 배열을 통한 조건부 실행
- useEffect는 두번째 인자로 dependency array를 받음.
- 이 배열에 지정된 변수나 값이 변경될 때만 useEffect 내의 코드가 실행
- 만약 의존성 배열을 비워두면 컴포넌트가 마운트 될 때 단 한 번만 실행
- 의존성 배열 자체를 생략하면 컴포넌트가 렌더링될 때마다 실행

    - 예시 1. 특정 상태 변경 감지 : 사용자 이름이 변경될 때마다 콘솔에 로그 출력
    ```js
      import React, { useState, useEffect } from 'react'
      function UserName({ name }) {
        useEffect(() => {
          console.log(`사용자 이름이 ${name}으로 변경됨`)
        }, [name])  // name 상태가 변경될 때마다 실행
        return <p>사용자 이름 : {name}</p>
    }
    ```

    - 예시 2. 여러 의존성 감지 : 사용자 이름과 나이가 변경될 때 작업을 수행
    ```js
      import React, { useState, useEffect } from 'react';
      function UserInfo({ name, age }) {
        useEffect(() => {
          console.log(`사용자 정보가 변경되었습니다. 이름: ${name}, 나이: ${age}`);
        }, [name, age]); // name 또는 age가 변경될 때 실행
        return (
          <div>
            <p>이름: {name}</p>
            <p>나이: {age}</p>
          </div>
        );
      }
    ```
    
    - 예시 3. 의존성 배열 없이 매 렌더링 후 실행 : 컴포넌트가 렌더링 될 때마다 실행되는 로그 기록
      ```js
        import React, { useEffect } from 'react'
        function LogRender() {
          useEffect(() => {
            console.log('컴포넌트가 렌더링됨')
          })  //의존성 배열이 없으므로 컴포넌트가 렌더링될 때마다 실행
          return <div>렌더링 로그 기록 예시</div>
        }
      ```

## Cleanup 함수 제공
-  useEffect 내에서 반환(return)하는 함수는 컴포넌트가 언마운트될 때 실행됨
-  이를 통해 구독을 해제하거나, 메모리 누수를 방지하기 위해 필요한 정리 작업을 수행할 수 있음
-  예) 이벤트 리스너 제거, 타이머 정리 

    - 예시 1. 이벤트 리스너 설정 및 제거 : 브라우저의 리사이즈 이벤트에 리스너를 추가하고 제거함
    ```js
      import React, { useState, useEffect } from 'react'
      function WindowSize() {
        const [size, setSize] = useState(window.innerWidth)
        useEffect(() => {
          function updateSize() {
            setSize(window.innerWidth)
          }
          window.addEventListener('resize', updateSize)
          return () => {
            window.removeEventListener('resize', updateSize)
          }
        }, [])  //의존성 배열이 비어 있으므로 컴포넌트 마운스 시에만 실행
    ```

    - 예시 2. 구독 해제 : 컴포넌트가 언마운트될 때 구독을 해제
    ```js
      import React, { useState, useEffect } from 'react'
      function SubScribe() {
        useEffect(() => {
          //구독 로직
          const subscription = dataSource.subscribe()
          return () => {
            //구독 해제 로직
            subscription.unsubscribe()
          }
        }, [])
        return <div>구독 및 구독 해제 예시</div>
      }
    ```

    - 예시 3. 타이머 정리 : 컴포넌트가 언마운트 될 때 setInterval을 정리
    ```js
      import React, { useEffect } from 'react'
      function Timer() {
        useEffect(() => {
          const timer = setInterval(() => {
            console.log('타이머 실행 중...')
          }, 1000)
          return () => clearInterval(timer)    //컴포넌트가 언마운트될 때 타이머 정리
        }, [])
        return <div>타이머 예시</div>
    ```






    
