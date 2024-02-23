# HTTP (HyperText Transfer Protocol)
- 웹에서 데이터를 주고받기 위해 사용되는 프로토콜
- 클라이언트와 서버 간의 통신을 가능하게 하여, 주로 HTML 문서, 이미지, 비디오, jSON, XML 등 다양한 형태의 리소스를 전송하는 데 사용됨

## 작동 원리
- HTTP는 요청/응답 프로토콜
- 클라이언트가 서버에 어떤 작업을 수행하도록 요청(request)하면, 서버는 해다아 요청을 처리한 후 결과를 클라이언트에게 응답(response)함

### 요청
- **메서드** : 클라이언트가 수행하길 원하는 동작
- **URI** : 요청이 가해지는 리소스의 위치
- **HTTP** : 클라이언트가 사용하는 HTTP 프토로콜의 버전
- **헤더** : 요청에 대한 추가 정보(예 : Host, User-Agent, Accept, Content-Type) 등
- **바디** : 일부 요청(주로 PUT, POST)에 포함되어 서버로 전송되는 데이트

### 응답
- 상태 코드와 이유 구절 : 요청이 성공했는지 여부를 나타내는 코드(예 : 200 OK, 404 Not Found)
- HTTP 버전 : 서버가 사용하는 HTTP 프로토콜 버전
- 헤더 : 응답에 대한 추가 정보(예 : Content-Type, Content-length, Set-Cookies등)
- 바디 : 클라이언트의 요청을 충족시키는 리소스나 정보


### HTTP 메서드
- GET : 지정된 리소스를 조회
  - 예시
    1. 단순한 데이터 요청
    ```js
    //express server
    app.get('/api/data', (req,res) => {
      res.json({message : 'Hello, World'})
    })

    //client vanilla javascript
    fetch('/api/data')
      .then(res => res.json())
      .then(data => console.log(data))
    ```
    2. 쿼리 파라미터를 포함한 요청
    ```js
    //express server
    app.get('api/search', (req,res) => {
      const query = req.query.query
      res.json({ searchResult : `Result for ${query}` })
    })
    //client vanilla javascript
    fetch('api/search?query=example')
      .then(res => res.json())
      .then(data => console.log(data))
    ```
    3. 경로 파라미터를 포함한 요청
    ```js
    //express server
    app.get('api/profile/:userId', (req,res) => {
      const userId = req.params.userId
      res.json({ userId : userId, userName : "Park" })
    })
    //client vanilla javascript
    fetch('api/profile/201')
      .then(res => res.json())
      .then(data => console.log(data))
    ```
- POST : 지정된 리소스에 데이터를 제출하여 처리를 요청함. 주로 데이터 생성에 사용
  - 예시
    1. JSON 데이터 전송
    ```js
    //express server
    app.post('api/data', (req,res) => {
      console.log(req.body)  
      res.json({ status : 'Success', received : req.body })
    })
    //client vanilla javascript
    fetch('api/data', {
      method : 'POST',
      headers : {
        'Content-Type' : 'application/json'
      },
      body : JSON.stringify({ message : 'Hello, World' })
      })
      .then(res => res.json())
      .then(data => console.log(data))
    ```
    2. 폼 데이터 전송
    ```js
    //express server
    app.post('api/formdata', (req,res) => {
      console.log(req.body)
      res.json({ status : 'Success', username : req.body.username })
    })
    //client vanilla javascript
    const formData = new FormData()
    formData.append('username' : 'park')
    formData.append('password' : '4044')
    fetch('api/formData', {
      method : 'POST',
      body : formData
      })
      .then(res => res.json())
      .then(data => console.log(data))
    ```
    3. 파일 업로드
    ```js
    //express server
    app.post('api/upload', upload.single('file'), (req,res) => {
      console.log(req.file)
      res.json({ status : 'Success', filename : req.file.originalname })
    })
    //client vanilla javascript
    const fileInput = document.querySelector('input[type="file"])
    const formData = new FormData()
    formData.append('file', fileInput.files[0])
    fetch('api/data', {
      method : 'POST',
      body : formData
      })
      .then(res => res.json())
      .then(data => console.log(data))
    ```
- PUT : 지정된 리소스를 업데이트
  - 예시
    1. 리소스 업데이트
    ```js
    //express server
    app.put('api/user/:id', (req,res) => {
      const userId = req.params.id
      const userData = req.body
      res.json({ message : `User ${userId} updated`, updatedData : userData })
    })
    //client vanilla javascript
    fetch('api/user/123', {
      methpd : 'PUT',
      headers : {
        'Content-Type' : 'application/json'
      },
      body : JSON.stringify({ name : 'Park', email : 'park@example.com' })
      })
      .then(res => res.json())
      .then(data => console.log(data))
    ```
    2. 특정 항목의 상태 변경
    ```js
    //express server
    app.put('api/task/:tastId/complete', (req,res) => {
      const taskId = req.params.taskId
      res.json({ message : `User ${userId} maked as complete` })
    })
    //client vanilla javascript
    fetch('api/task/123/complete', {
      methpd : 'PUT',
      })
      .then(res => res.json())
      .then(data => console.log(data))
    ```
    3. 설정 변경
    ```js
    //express server
    app.put('api/settings', (req,res) => {
      const settings = req.body
      res.json({ message : 'Settings updated' , newSettings : settings })
    })
    //client vanilla javascript
    fetch('api/settings', {
      methpd : 'PUT',
      headers : {
        'Content-Type' : 'application/json'
      },
      body : JSON.stringify({ theme : 'dark', notifications : 'enabled' })
      })
      .then(res => res.json())
      .then(data => console.log(data))
    ```
- DELETE : 지정된 리소스 삭제
  - 예시
    1. 특정 사용자 삭제
    ```js
    // express server
    app.delete('/api/user/:id', (req,res) => {
      const userId = req.params.id
      res.json({ message : `User ${userId} deleted` })
    })
  
    // client vanilla javascript
    fetch('/api/user/123', {
      method : 'DELETE'
      })
      .then(res => res.json())
      .then(data => console.log(data))
    ```
    2. 특정 게시글 삭제
    ```js
    // express server
    app.delete('/api/post/:postId', (req,res) => {
      const postId = req.params.postId
      res.json({ message : `Post ${postId} deleted` })
    })
  
    // client vanilla javascript
    fetch('/api/post/123', {
      method : 'DELETE'
      })
      .then(res => res.json())
      .then(data => console.log(data))
    ```
    3. 사용자 설정 초기화
    ```js
    // express server
    app.delete('/api/user/:id/setting', (req,res) => {
      const userId = req.params.id
      res.json({ message : `settings for user ${userId} reset` })
    })
  
    // client vanilla javascript
    fetch('/api/user/123/settings', {
      method : 'DELETE'
      })
      .then(res => res.json())
      .then(data => console.log(data))
    ```
- PATCH : 리소스의 부분적인 수정 수행
  - 예시
    1. 사용자 정보 부분 업데이트
    ```js
    // express server
    app.patch('/api/user/:id', (req,res) => {
      const userId = req.params.id
      const updates = req.body
      res.json({ message : `User ${userId} updated`, updatedData : updates })
    })

    // client vanilla javascript
    fetch('/api/user/1234', {
      method : 'PATCH',
      headers : {
        'Content-Type' : 'application/json'
      },
      body : JSON.stringify({ email : 'park@example.com' })
      })
      .then(res => res.json())
      .then(data => console.log(data))
    ```
    2. 특정 게시글의 특정 필드 수정
    ```js
    // express server
    app.patch('/api/post/:postId', (req,res) => {
      const postId = req.params.postId
      const updates = req.body
      res.json({ message : `Post ${userId} updated`, updatedData : updates })
    })

    // client vanilla javascript
    fetch('/api/post/1234', {
      method : 'PATCH',
      headers : {
        'Content-Type' : 'application/json'
      },
      body : JSON.stringify({ title : 'Updateed Post Title' })
      })
      .then(res => res.json())
      .then(data => console.log(data))
    ```
    3. 사용자 설정의 특정 부분 변경
    ```js
    // express server
    app.patch('/api/user/:id/settings', (req,res) => {
      const userId = req.params.id
      const settingsUpdate = req.body
      res.json({ message : `Setting for user ${userId} updated`, newSettings : settingsUpdate })
    })

    // client vanilla javascript
    fetch('/api/user/1234/settings', {
      method : 'PATCH',
      headers : {
        'Content-Type' : 'application/json'
      },
      body : JSON.stringify({ notifications : false })
      })
      .then(res => res.json())
      .then(data => console.log(data))
    ```
- HEAD : GET 요청과 동일하지만, 응답 본문 없이 헤더 정보만 반환
- OPTIONS : 대상 리소스에 대해 통신 옵션 설명
- CONNECT : 프록시 기능을 요청할 때 사용되며, 요청한 리소스로의 터널을 설정하기 위해 사용
- TRACE : 클라이언트의 요청을 서버로 보내고, 경로를 따라 중간에 위치한 서버들이 수행하는 변경 없이 그대로 다시 클라이언트에게 되돌려 보내는 루프백 테스트에 사용


### 상태 코드
- 1xx (정보 응답) : 요청을 받았으며 프로세스를 계속 진행함
  - 100 Continue : 이 임시 응답은 클라이언트가 요청을 계속해야 하거나 요청이 이미 완료된 경우 응답을 무시해야함을 나타냄
  - 101 Switchng Protocols : 클라이언트로부터의 업그레이트 요청 에더에 대한 응답으로, 서버가 전환하는 프로토콜을 나타냄
  - 102 Processing(WebDAV) : 서버가 요청을 받아 처리 중이지만 아직 응답이 준비되지 않았음을 나타냄
  - 103 Early Hints : 주로 링크 헤더와 함께 사용하기 위한 것으로, 서버가 응답을 준비하는 동안 사용자 에이전트가 리소스 사전 로드를 시작하거 페이지에 리소스가 필요한 출처에 미리 연결할 수 있도록 함
  -  
- 2xx (성공) : 요청이 성공적으로 받아들여짐
  - 200 OK : 요청 성공. "성공"의 의미는 HTTP 메서드에 따라 다름
    - `GET` : 리소스를 가져와서 메시지 본문으로 전송함
    - `HEAD` : 표현 헤더가 메시지 본문 없이 응답에 포함
    - `PUT` or `POST` : 작업 결과를 설명하는 리소스가 메시지 본문에 전송
    - `TRACE` : 메시지 본문에는 서버에서 수신한 요청 메시지가 포함
  - 201 Created : 요청이 성공하고 새 리소스 생성
  - 202 Accepted : 요청은 받아들여졌지만 아직 처리되지 않음.
  - 203 Non-Authoritative information : 반환된 메타데이터가 원본 서버에서 사용 가능한 것과 정확히 동일하지 않지만 로컬이나 제3자 사본에서 수집된 것임을 나타냄
  - 204 No Content : 요청에 보낼 콘텐츠가 없지만 헤더는 유용할 수 있음. 사용자 에이전트는 이 리소스에 대한 캐시된 헤더를 새로운 것으로 업데이트 할 수 있음
  - 205 Reset Content : 이 요청을 보낸 문서를 재설정하라고 사용자 에이전트에게 알림
  - 206 Partial Content : 리소스의 일부만 요청하기 위해 클라이언트에서 Range 헤더를 보낼 때 사용
  - 207 Multi-Status(WebDAV) : 여러 리소스에 대한 정보를 전달하며 여러 상태 코드가 적절한 상황에 사용
  - 208 Already Reported(WebDAV) : 같은 컬렉션에 대한 여러 바인딩의 내부 멤버를 반복적으로 나열하는 것을 피하기 위해 응답 요소 내에서 사용
  - 226 IM Used(HTTP Delta encoding) : 서버가 리소스에 대한 요청을 완수했고 응답은 현재 인스턴스에 적용된 하나 이상의 인스턴스 조작의 결과를 나타냄
- 3xx (리다이렉션) : 요청을 완료하기 위해 추가 작업이 필요
  - 300 Multiple Choices
  - 301 Moved Permanently : 요청한 리소스가 영구적으로 새 위치로 이동함. 클라이언트는 앞으로 이 리소스에 대한 요청을 새 URL로 보내야함
  - 302 Found : 요청한 리소스가 일시적으로 다른 URL에 위치해 있음을 나타냄
  - 303 See Other
  - 304 Not Modified : 클라이언트가 조건부 GET 요청을 했고, 그 조건이 충족되지 않았을 때 전송됨. 즉, 클라이언트의 캐시된 버전이 여전이 유효함
  - 307 Temporary Redirect
  - 308 Permanent Redirect
- 4xx (클라이언트 에러) : 클라이언트 측에서 오류 발생
  - 400 Bad Request : 서버가 요청을 이해할 수 없음을 나타냄. 잘못된 요청 구조로 인해 발생할 수 있음
  - 401 Unauthorized : 요청이 인증을 필요로 하며, 클라이언트가 그러한 인증을 제공하지 않음
  - 402 Payment Required
  - 403 Forbidden : 서버가 요청을 이해했으나, 클라언트가 그러한 인증을 제공하지 않음
  - 404 Not Found : 서버가 요청한 리소스를 찾을 수 없음을 나타냄
  - 405 Method Not Allowd
  - 406 Not Acceptable
  - 407 Proxy Authentication Required
  - 408 Request Timeout
  - 409 Conflict
  - 410 Gone
  - 411 Length Required
  - 412 Precondition Failed
  - 413 Payload Too Large
  - 414 URI Too Long
  - 415 Unsupported Media Type
  - 416 Range Not Satisfiable
  - 417 expectation Failed
  - 418 I'm a teapot : 1998년 만우절을 맞이하여 정의된 코드. 서버가 주전자이며, 클라이언트가 커피를 끓이라는 요청을 보냈지만, 해당 장치는 주전자이므로 해당 작업을 수행할 수 없음을 의미
  - 421 Misdirected Request
  - 422 Unprocessable Content
  - 423 Locked
  - 424 Failed Dependency
  - 425 Too Early
  - 426 Upgrade Required
  - 428 Precondition Required
  - 429 Too Manyy Request
  - 431 Request header Fields Too Large
  - 451 Unavailalbe For Legal Reasons
- 5xx (서버 에러) : 서버가 유효한 요청을 처리하지 못함
  - 500 Internal Server Error : 서버가 요청을 처리하는 중 예상치 못한 상황을 만났을 때 발생함
  - 501 Not Implemented : 서버가 요청으 메서드를 지원하지 않거나 구현할 수 없음을 나타냄
  - 502 Bad Gateway : 서버가 게이트웨이나 프록시 역할을 하며, 상류 서버로부터 유효하지 않은 응답을 받았음을 나타냄
  - 503 Service Unavailable : 서버가 일시적으로 요청을 처리할 준비가 되어 있지 않음을 나타냄. 보통 유지 보수 또는 오버로딩 때문에 발생
  - 504 Gateway Timeout : 서버가 게이트웨이나 프록시 역할을 하며, 상류 서버로부터 시간 내에 응답을 받지 못했음을 나타냄
  - 505 HTTP Version Not Supported
  - 506 Variant Also Negotiates
  - 507 Insufficient Storage
  - 508 Loop Detected
  - 510 Not Extended
  - 511 Network Authentication Required

 #### status code의 번호가 비연속적인 이유
 1. HTTP 프로토콜은 확장성을 고려하여 설계됨. 새로운 상태 코드를 필요에 따라 추가할 수 있는 유연성을 제공하기 위함. 비연속적인 번호 할당은 미래의 확장을 위해 일부 번호 범위를 미리 예약하거나 비워 둘 수 있는 공간을 제공함
 2. HTTP 프로토콜이 발전하면서 일부 상태 코드들은 더 이상 사용되지 않게 되었거나, 다른 코드로 대체됨.
 3. 상태 코드는 코드들이 나타내는 응답의 성격에 따라 범주화됨(예 : 1xx, 2xx, 3xx, 4xx)


### HTTP vs HTTPS
- HTTP는 암호화되지 않은 텍스트로 데이터를 전송하기 때문에, 중간자 공격(man-in-the-middle)에 취약함
- 이를 해결하기 위해, HTTPS(HTTP Secure)가 도입됨
- HTTPS는 SSL(Secure Socket Layer)또는 TLS(Transport Layer Security) 프로토콜을 사용하여 클라이언트와 서버 간의 통신을 암호화함
  


































