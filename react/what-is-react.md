# React
- 페이스북에서 개발한 오픈 소스 프론트엔드 라이브러리
- 사용자 인터페이스를 만들기 위한 JavaScript 라이브러리
- 단일 페이지 어플리케이션이나 모바일 애플리케이션 개발에서 주로 사용, 가상 DOM을 활용하여 성능 최적화


## 가상 DOM 
실제 DOM 조작을 최소화하여 성능을 향상. 가상 DOM은 실제 DOM과 동기화되며, UI 업데이트 시에 변경된 부분만 업데이트함
```js
import React, { useState } from 'react'
import ReactDOM from 'react-dom'

function App() {
  const [count, setCount] = useState(0)
  const handleClick = () => {
    setCount(count + 1)
  }
  return (
    <div>
      <h1>카운터: {count}</h1>
      <button onClick={handleClick}>증가</button>
    </div>
  )
}
ReactDom.render(<App/>, document.getElementById('root'))
```
- 위 코드에서 `useState` 훅을 사용하여 상태를 관리하고, `handleClidk`함수를 사용하여 버튼 클릭 시 상태를 업데이트함
- 사용자가 버튼을 클릭하면, 상태가 업데이트되고, `render`함수가 호출됨
- 이때 리액트는 이전 가상 DOM 트리와 현재 가상 DOM 트리를 비교하여 변경된 부분을 실제 DOM에 반영함


## 컴포넌트 기반 아키텍쳐
- UI를 작은 컴포넌트로 나누어 개발함
- 각 컴포넌트는 독립적이며 재사용이 가능함. 이를 조합하여 복잡한 UI를 구축할 수 있음
```js
import React, { useState } from 'react'
import ReactDOM from 'react-dom'

function ListItem({ value }) {
  return <li>{value}</li>
}
function List({ items }) {
  return (
    <ul>
      {items.map((item, index) => (
        // 각 아이템을 ListItem 컴포넌트로 변환합니다.
        <ListItem key={index} value={item} />
      ))}
    </ul>
  )
}

const listItems = ['list1', 'list2', 'list3']
ReactDom.render(<List items={listItems} />, document.getElementById('root'))
```
- 위 코드에서 `List`컴포넌트는 `items` props를 받아서 리스트를 렌더링함
- `ListItem`컴포넌트는 각각의 리스트 아이템을 렌더링함

## 단방향 데이터 흐름 (Unidirectional Data Flow)
- 데이터는 부모 컴포넌트에서 자식 컴포넌트로만 전달되며, 애플리케이션의 상태를 예측 가능하고 유지보수가 쉽게 만듦
```js
import React, { useState } from 'react'
import ReactDOM from 'react-dom'

function ChildComponent({ data }) {
  return <p>자식 컴포넌트에서 받은 데이터: {data}</p>
}

function ParentComponent() {
  const [data, setData] = useState('')

  const handleChange = () => {
    setData('새로운 데이터')
  };

  return (
    <div>
      <button onClick={handleChange}>데이터 변경</button>
      <ChildComponent data={data} />
    </div>
  )
}

ReactDOM.render(<ParentComponent />, document.getElementById('root'))
```

## JSX (JavaScript XML)
- JavaScript 코드 안에 HTML과 유사한 마크업을 작성할 수 있게함
```js
import React from 'react'
import ReactDOM from 'react-dom'

const MyComponent = () => {
  const name = 'John Doe'
  const age = 30

  return (
    <div>
      <h1>Hello, {name}!</h1>
      <p>You are {age} years old.</p>
    </div>
  )
}

ReactDOM.render(<MyComponent />, document.getElementById('root'))
```
- 위 코드에서 `<h1>`, `<p>` 태그 등 HTML과 유사한 마크업을 작성할 수 있음
- JSX는 JavaScript 코드 안에 포함되어 있지만, HTML과 유사한 구문을 사용하여 컴포넌트의 UI를 정의함
- JSX 내부에서 중괄호 `{}`를 사용하여 JavaScript 표현식(변수, 함수)을 사용할 수 있음

## 단일 페이지 어플리케이션 (Single Page Application, SPA)
- 브라우저에서 페이지 전체를 새로고침하지 않고도 동적으로 페이지를 업데이트할 수 있음
```js
import React from 'react'
import ReactDOM from 'react-dom'
import { BrowserRouter as Router, Route, Link } from 'react-router-dom'

const Home = () => (
  <div>
    <h1>홈 페이지</h1>
    <p>이 페이지는 홈 페이지입니다.</p>
  </div>
)
const About = () => (
  <div>
    <h1>소개 페이지</h1>
    <p>이 페이지는 소개 페이지입니다.</p>
  </div>
)
const App = () => (
  <Router>
    <div>
      <nav>
        <ul>
          <li><Link to="/">홈</Link></li>
          <li><Link to="/about">소개</Link></li>
        </ul>
      </nav>
      <Route exact path="/" component={Home} />
      <Route path="/about" component={About} />
    </div>
  </Router>
)

ReactDOM.render(<App />, document.getElementById('root'))
```
- 위 코드에서 React Router를 사용하여 SPA를 구현함
- `BrowserRouter`를 사용하여 라우터를 설정하고 `Route` 컴포넌트를 사용하여 경로와 해당 컴포넌트를 매핑함
- `Link` 컴포넌트를 사용하여 각 페이지로의 링크 제공
- 사용자가 링크를 클릭하면 페이지가 새로고침되지 않고도 해당 컴포넌트가 동적으로 렌더링됨

## 재사용 가능한 컴포넌트
- 컴포넌트는 다양한 환경에서 재사용할 수 있음
```js
import React from 'react'

const Button = ({ onClick, children }) => {
  return (
    <button onClick={onClick}>
      {children}
    </button>
  )
}

const App = () => {
  const handleClick = () => {
    alert('버튼이 클릭되었습니다!')
  }

  return (
    <div>
      <h1>버튼 예시</h1>
      {/* 버튼 컴포넌트를 사용하여 버튼을 렌더링합니다. */}
      <Button onClick={handleClick}>클릭하세요!</Button>
    </div>
  )
}

export default App
```
- 위코드에서 `Button`컴포넌트는 재사용 가능한 버튼을 정의함
-  `onClick` prop으로 전달된 함수를 클릭 이벤트에 연결하고, 버튼의 내용은 `children` prop을 통해 동적으로 받음
-  `App` 컴포넌트에서는 `Button` 컴포넌트를 사용하여 버튼을 렌더링함. 이렇게 함으로써 `Button` 컴포넌트를 여러번 재사용할 수 있음
-  버튼의 모양과 동작은 `Button` 컴포넌트 안에서 일관되게 정의됨


















