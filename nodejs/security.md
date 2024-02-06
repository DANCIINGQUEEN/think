# 간단한 보안 강화 미들웨어

## 1. Helmet 
Helmet은 여러 보안 관련 HTTP 헤더를 설정하여 애플리케이션의 보안을 강화
  - **Content Security Policy(CSP)** : 외부 소스로부터 악의적인 스크립트 주입 공격을 방지하기 위해, 어떤 종류의 콘텐츠가 어디서 로드될 수 있는지 정의
    - 리소스 출처 제한 : CSP를 사용하면 웹 페이지에서 로드되는 스크립트, 스타이르 이미지 및 기타 리소스의 출처(origin)을 제한할 수 있음
    - 인라인 스크립트 제한 : XSS(Cross-Site-Scripting) 공격을 방지함. 인라인 스크립트는 HTML 속성과 이베트 핸들러에서 직접 실행되는 스크립트
    - 이벤트 핸들러 제한 : 특정 이벤트 핸들러를 사용하는 것을 제한할 수 있음. 예를 들어 "onclick" 이벤트 핸들러를 특정 출처에서만 실행하도록 설정할 수 있음
    - 보고 기능 : 브라우저에서 보안 정책 위반 사례르르 보고하도록 설정할 수 있음. 이를 통해 애플리케이션의 보안 무네를 식별하고 해결할 수 있음
  - **X-Content-Type-Options** : 브라우저가 MIME 타입을 추측하지 못하게 하여 MIME 타입 혼동 공격 방지
    - MIME(MultiPurpose Internet Mail Extensions) Type : 다양한 멀티미디어 데이터 형식을 식별하고 표시하기 위한 표준 인터넷 미디어 타입
      - HTML 문서 : `text/html` type
      - JPEG 이미지 : `image/jpeg` type
  - **X-Frame-Options** : 클릭재킹 공격으로부터 보호하기 위해, 페이지가 `<frame>`, `<iframe>`, `<object>`, `<embed>` 또는 `<applet>` 태그 안에서 렌더링되는 것을 방지
    - X-Frame-Options : 웹 페이지를 다른 웹 사이트의 프레임(frame) 내에서 로드되는것을 제어함
      - DENY : 다른 웹 사이트에서 현재 페이지를 프레임으로 불러올 수 없음
      - SAMEORIGIN : 현재 웹 사이트와 동일한 출처(origin)에서만 현재 페이지를 프레임으로 불러올 수 있음. 다른 도메인에서는 프레임화할수 없음
      - ALLOW-FROM uri : 특정 URI(Uniform Resource Identifier)에서만 현재 페이지를 프레임화할 수 잇도록 허용
  - **X-Powered-By** : Express 애플리케이션을 더 덜 식별 가능하게 만들기 위해 `X-Powered-By` 헤더를 제거
    - X-Powered-By : 웹 서버나 프레임워크가 어떤 소프트웨어나 기술로 구동되고 있는지를 클라이언트(브라우저)에게 알려주는 역할. 이 헤더는 보안과 개인 정보 보호 측면에서 공격자에게 추가 정보를 노출시킬 수 있으므로, 일반적으로 보안 관련 이슈 때무에 미사용이 권장

## 2. Express-rate-limit
Express 애플리케이션에 요청 속도 제한 기능을 추가하는 미들웨어
  - 
