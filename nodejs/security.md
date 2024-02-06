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
  - **브루트 포스 공격 방지** : 사용자 인증 같은 특정 경로에 대해 무차별 대입 공격을 방지하기 위해 요청 수를 제한
    - 브루트 포스 공격(Brute Force Attack) : 암호나 인증 정보를 찾아내기 위해 모든 가능한 조합을 시도하는 공격 기법
      - 공격자는 암호, PIN, 인증 토큰 또는 다른 비밀 정보를 발견하기 위해 여러 시도를 수행
      - 모든 가능한 조합 시도 : 공격자는 모든 가능한 문자, 숫자 및 기호 조합을 시도하여 올바른 비밀 정보를 찾을 때까지 계속함
      - 암호 무력화 : 사용자의 암호를 알아내어 계정이 불법적으로 액세스하려고 시도
      - 시간과 리소스 필요 : 암호가 강력한 경우, 브루트 포스 공격은 매우 오랜 시간과 컴퓨팅 리소스를 필요로함
      - 방어 및 예방 : 암호의 복잡성을 높이고, 계정 잠금 정책을 적용하여 일정 횟수 실패한 로그인 시도 후에 계정을 잠그는 등의 보안 조치를 취할 수 있음
  - **DDos 공격 완화** : 서버에 과도한 트래픽이 발생하는 것을 방지하기 위해, 각 IP 주소별로 요청의 수를 제한
    - DDos 공격 : 여러 컴퓨터 또는 기기를 사용하여 대상 서버 또는 네트워크에 대량의 트래픽을 동시에 보내 웹 서비스나 네트워크를 마비시키거나 사용 불가능하게 만드는 공격
      - 분산 공격 : 공격자는 여러 컴퓨터, 봇넷, 또는 감염된 기기를 사용하여 공격을 수행. 여러 출처에서 공격 트래픽이 발생하므로 대상을 방어하기 어려워짐
      - 대역폭 공격 : 고용량 대역폭을 사용하여 대상 시스템에 공격 트래픽을 덮치는 것. 대상 서버 또는 네트워크의 대역폭을 초과하거나 과부하를 초래하여 서비스를 마비시킴
      - 서비스 거부 : 목표로 하는 서비스 또는 웹사이트에 대한 액세스를 거부하는 것을 목표로 함. 이로 인해 정상 사용자가 해당 서비스를 이용할 수 없게 됨
      - 다양한 유형 : HTTP Flooding, SYN Flooding, UDP Flooding, ICMP Flooding...
      - 방어 및 감지 : CDN(Content Delivery Network), 방화벽, 인라인 IPS(Intrusoin Prevention System) 등의 보안 솔류션을 사용하여 공격을 막을 수 있음

## 3. HPP (HTTP Parameter Pollution Protection)
HTTP 요청에서 동일한 파라미터가 여러 번 사용될 때 발생하는 문제를 해결
  - 요청 URL이 `?name=park&name=lee`와 같이 동일한 파라미터가 중복되어 있을 때, HPP는 요청을 적절히 처리하여 애클리케이션 로직에 영향을 주지 않도록 함


```js
import helmet from 'helmet';
import rateLimit from 'express-rate-limit';
import hpp from 'hpp';
import cors from 'cors';

export const setupSecurity = (app) => {
    // Helmet을 사용하여 여러 보안 관련 HTTP 헤더 설정
    app.use(helmet());

    // 기본 CORS 설정
    app.use(cors());

    // Rate Limiting 설정
    const limiter = rateLimit({
        windowMs: 15 * 60 * 1000, // 15분
        max: 100 // 15분 동안 최대 100개의 요청 허용
    });
    app.use(limiter);

    // HPP를 사용하여 HTTP Parameter Pollution 공격 방지
    app.use(hpp());
};
```
