```js
app.use(express.json())
app.use(express.urlencoded({extended : false})
app.use(cookieParser())
```

## express.json()
들어오는 요청의 본문(body)이 JSON 형식일 때 이를 파싱하는 역할
- 즉 클라이언트로부터 전송되 JSON 데이터를 자동으로 파싱하여, `req.body`를 통해 사용할 수 있도록 함

## express.urlencoded({ extended : false })
URL 인코딩된 본문을 파싱하는 역할
- `extended : false` : 본문 파싱에 `querystring` 라이브러리를 사용하겠다는 의미
- 예 : 클라이언트가 `<form>` 태그를 통해 전송한 데이터를 서버에서 파싱하여 사용할 수 있음


## cookieParser()
요청에 동봉된 쿠키를 파싱하는 역할
- `req.cookies` 를 통해 클라이언트로부터 전송된 쿠키를 쉽게 추출하고 사용할 수 있음
- 예 : 인증, 사용자 세션 관리, 사용자 선호도 저장 등의 목적으로 클라이언트에서 보낸 쿠키를 서버에서 읽을 필요가 있을 때 사용
