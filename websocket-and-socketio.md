# WebSocket
- 웹에서 양방향 통신을 가능하게 하는 고급 기술
- 클라이언트와 서버 간에 지속적인 연결을 설정하여, 데이터를 양쪽으로 실시간으로 주고받을 수 있음

  ## 특징
    -  실시간 통신 : 서버와 클라이언트 간의 실시간 데이터 전송을 가능하게 함
    -  프로토콜 : `ws`(비암호화) 또는 `wss`(암호화) 프로토콜 사용
    -  양방향 통신 : 데이터는 섭와 클라이언트 양쯕으로 흐를 수 있음
    -  효율적인 성능 : 지속적인 연결을 유지함으로써 HTTP의 오버헤드를 줄임
 
  ## WebSocket(ws)
    - 비암호화된 통신을 제공, URL은 "ws://" 로 시작
    - 초기 연결 설정 후에 양방향 데이터 전송을 위한 지속적인 연결 유지
    - 서버 푸시, 실시간 채팅, 온라인 게임 및 주식 시장 데이터와 같은 실시간 기능을 구현할 때 유용
  ## WebSocket Secure(wss)
    - WebSocket의 보안 버전. 데이터를 암호화하여 보호하는 역할
    - TLS/SSL(Transport Layer Security / Secure Sockets Layer)을 사용하여 통신을 암호화
    - 민감한 정보나 보인이 중요한 애플리케이션에서 사용됨. 데이터의 무단 엑세스나 감청을 방지

```js
const fs = require('fs')
const https = require('https')
const Ws = requrie('ws')

//SSL/TLS 인증서 로드
const server = https.createServer({
  cert: fs.readFileSync('path/to/cert.pem'),
  key: fs.readFileSync('path/to/key.pem')
})

const wss = new Ws.Server({ server })

wss.on('connection', function connection(ws) {
  console.log('client connected')

  ws.on('message', function incoming(message) [
    console.log('message: %s', message)
    //클라이언트에서 메시지를 echo함
    ws.send(`echo message ${message}`)
  })

  //연결 예외 처리 
  ws.on('error', (error) => {
    console.error('websocket error:', error)
  })

  //연결 종료 로깅
  ws.on('close', () => {
    console.log('client connection close')
  })
})
server.listen(8080, () => {
  console.log('서버 실행 중');
});
```


# Socket.io
- WebSocket을 기반으로 하는 라이브러리
- 웹소켓 이외의 여러 통신 방식을 지원
- WebSocket이 지원되지 않는 경우에도 통신을 가능하게 하기 위해 long-polling 등의 방법을 이용
  - Long-Polling 작동 방식
      1. 클라이언트가 서버에 HTTP 요청을 보냄
      2. 서버는 이 요청을 받고 클라이언트가 새로운 정보를 수신할 때까지 대기함
      3. 새로운 정보가 도착하면 서버는 해당 정보와 함께 HTTP 응답을 클라이어트에게 보냄
      4. 클라이언트는 새로운 정보를 처리하고 다시 서버에 HTTP 요청을 보냄
- 자동 재연결 지원 : 연결이 끊어졌을 때 자동으로 재연결 시도
- 방 기능 : 사용자들을 다양한 '방'으로 분류하여 통신을 구성할 수 있음
- 이벤트 기반 통신 : 사용자 정의 이벤트를 생성하여 복잡한 통신 패턴을 구현할 수 있음


```js
const http = require('http').createServer()
const io = require('socket.io')(http, {
  cosrs : {
    origin : "*",     //개발 목적으로 모든 출처 혀옹, 실제 배포 시에는 수정 필요
  }
})

io.ona('connection', (socket) => {
  console.log('클라이언트 연결', socket.id)

  //사용자가 방에 입장
  socket.on('joinRoom', (room) => {
    socket.join(room)
    console.log(`${socket.id}가 ${room} 방에 입장`)
    io.on(room).emit('message', `${socket.id} 방에 입장`)
  })

  //방에서 메시지 수신
  socket.on('message', (data) => {
    console.log(`방 ${data.room}에서 메시지 수신 : ${data.message}`)
    //같은 방의 다른 클라이언트에게 메시지 전송
    socket.to(data.room).emit('message', data.message)
  })

  //사용자가 방을 떠남
  socket.on('leaveRoom', (room) => {
    socket.leave(room)
    console.log(`${socket.id}가 ${room} 방에서 퇴장`)
    io.to(room).emit('message', `${socket.id}가 방을 떠남`)
  })

  //연결 해제
  socket.on('disconnect', () => {
    console.log(`${socket.id} 연결 해제`)
  })

  //예외 처리
  socket.on('error', (e) => {
    console.error(`error : ${e})
  })
})
http.listen(3000, () => {
  console.log('서버 실행 중')
})
```


# WebSocket과 Socket.io의 차이점
1. 호환성 : WebSocket은 표준 프로토콜이지만, 모든 웹 브라우저 또는 환경에서 지원되지 않을 수 있음. 반면 Socket.io는 더 많은 환경에서 작동할 수 있도록 설계됨
2. 기능성 : Socket.io는 WebSocket을 포함한 여러 방법을 사용하여 통신하고, 추가적인 기능 제공
3. 용도 : WebSocket은 기본적인 양방향 통신이 필요할 때 적합. Socket.io는 더 복잡하고 다양한 요구 사항을 가진 애플리케이션에 적합
