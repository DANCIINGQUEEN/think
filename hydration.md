# Hydration
- SSR(서버 사이드 렌더링) 또는 SSG(정적 사이트 생성)으로 생성된 HTML에 대해 클라이언트 사이드에서 이벤트 리스너와 같은 JavaScript 기능을 "활성화"하는 과정
  - SSR : 서버에서 사용자의 요청에 따라 실시간으로 HTML 페이지를 생성하고, 이를 사용자에게 전송. 사용자가 페이지를 요청할 때마다 새로운 HTML이 생성되기 때문에, 동적인 컨텐츠를 처리할 수 있음
  - SSG : 빌드 타임에 모든 페이지를 미리 HTML로 생성하고, 사용자의 요청 시에 이를 제공. 변경되지 않는 콘텐츠에 적합. 서버의 부하를 줄이고, 빠른 페이지 로드 속도 제공


## Hydration의 필요성
- 클라이언트 사이드에서 JavaScript를 로딩하고 실행하여, 서버에서 전송된 정적 HTML에 동적인 기능을 추가함
## Hydration 과정
1. SSR
   - 사용자가 웹 사이트에 접속하면, 서버는 SSR, SSG를 통해 생성된 정적 HTML을 클라이언트에게 전송함
   - 이 HTML에는 웹 페이지의 구조와 초기 콘텐츠가 포함되어 있음
   - 검색 엔진 최적화에 유리
2. 클라이언트에서 JavaScript 로딩
   - 사용자의 브라우저가 HTML을 받고 나면, 페이지에 포함된 JavaScript파일들을 로딩하기 시작함
   - 이 JavaScript에는 리액트와 같은 라이브러리 또는 프레임워크 코드 뿐만 아니라, 애플리케이션의 동적인 기능을 구현하는 코드도 포함됨
3. 하이드레이션 초기화
   - JavaScript가 로딩되고 실행되면, 리액트와 같은 라이브러리는 서버에서 받은 HTML을 기반으로 초기 컴포넌트 트리를 구성함
   - 그 다음, 이 컴포넌트 트리에 이벤트 핸들러와 같은 동적 기능을 연결하여, 사용자와의 상호작용을 처리할 수 있게됨
4. 동적 상호작용 활성화
   - hydration 과정이 완료되면, 페이지는 완전이 인터렉티브해짐
   - 사용자는 버튼을 클릭하거나 폼을 제출하는 등의 동작을 수행할 수 있으며, 이러한 동작을 클라이언트 사이드에서 처리되어 동적인 사용자 경험을 제공함


### hydration의 장점
- 성능 향상 : 사용자에게 빠르게 초기 콘텐츠를 제공함으로써 (사용자가 인지하는)성능을 향상시킴
- SEO 최적화 : SSR된 페이지는 검색 엔진이 쉽게 인덱싱할 수 있어 유리
- 점진적인 상호작용 : 페이지의 핵심 콘텐츠는 빠르게 사용자에게 제공되며, 나머지 JavaScript는 필요할 때 점진적으로 로딩되어 페이지의 상호작용성을 활성화