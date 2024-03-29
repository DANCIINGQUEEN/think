# `useState`를 `const`로 선언하는 이유

1. `useState`와 `const` 사용 이유 :
   - `useState` 훅은 컴포넌트의 상태를 관리하기 위한 리액트 훅
   - `useState`는 상태값과 그 상태를 업데이트하는 함수를 배열로 반환
   - `useState`의 상태 설정 함수는 비동기적으로 작동하며, 컴포넌트를 리렌더링할 때 새로운 상태 값으로 업데이트
   - `const`는  JavaScript에서 상수를 선언할 때 사용하는 키워드로, 선언된 변수의 재할당을 방지
   - `useState`를 사용할 때 `const`로 선언하는 것은 `state`와 `setState`가 초기화 이후 재할당되지 않도록 보장하기 위함
   - 즉 `state`와 `setState`는 해당 컴포넌트 내에서 동일한 참조를 유지하며, 이들의 식별자가 다름 값으로 재할당되는것을 방지
  
2. 변수 변경 가능성
   - `const`는 ES6에서 도입된 키워드로, 변수를 재할당할 수 없게 만듦. 이는 변수가 가리키는 초기 메모리 주소를 변경할 수 없음을 의미
   - `const`로 선언된 변수는 재할당될 수 없지만, 이는 변수가 가리키는 객체나 배열의 내용이 불변임을 의미하지 않음
   - 리액트의 `useState`에서 반환된 `state`는 불변 변수임. 즉, `state`자체를 직접 수정할 수 없음.
   - 그러나 `setState`함수를 사용하여 `state`값을 '업데이트'할 수 있음
   - `setState`함수를 호출하면 리액트는 새로운 상태 값으로 컴포넌트를 재렌더링함
   - 이 과정에서 `state` 변수는 새로운 값으로 '교체'되지만, 변수 자체의 재할당은 발생하지 않음
   - `const`로 선언된 상태 설정 함수는 메모리 주소가 변하지 않기 때문에, 컴포넌트의 리렌더링 동안 동일하게 유지
