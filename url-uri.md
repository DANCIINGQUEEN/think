# URL (Uniform Resource Locator)
- 웹 상의 자원의 위치를 나타냄. 해당 자원에 접근하기 위한 구체적인 방법을 제공
- 자원이 위치한 서버의 주소와 해당 서버에서 자원을 어떻게 접근할 수 있는지에 대한 정보를 포함함
- URL 구조
  - 프로토콜 : 자원에 접근하기 위해 사용되는 통신 규약 (예 : http, https, ftp)
  - 호스트 이름 : 자원을 호스팅하는 서버의 이름 또는 IP주소
  - 포트 번호(선택적) : 서버에서 자원에 접근하기 위해 사용되는 포트 번호
  - 경로 : 서버 내에서 자원의 위치를 지정하는 경로
  - 쿼리 문자열(선택적) : 자원에 접근할 때 제공되는 추가 파라미터. ? 로 시작하고 &으로 구분. 파라미터 이름과 값의 쌍으로 구성
  - 프래그먼트(선택적) : 자원 내의 특정 부분을 직접 참조할 때 사용. URL의 마지막 부분에 #기호에 이어서 작성됨
- 예 1 : https://en.wikipedia.org/wiki/Uniform_Resource_Identifier#Syntax
- 예 2 : https://www.examplebookstore.com/search?category=books&query=programming&sort=newest



# URI (Uniform Resource Identifier)
- 인터넷 상의 자원을 식별하기 위한 문자열 구조
- URL과 URN(Uniform Resource Name)을 포함하는 더 넓은 개념
- 모든 URL은 URI이지만, 모든 URI가 URL은 아님


## 차이점
- **용도** : URL은 자원의 위치와 접근 방법을 제공함. URI는 자원을 단순히 식별하며, 이는 위치(URL) 또는 이름(URN)일 수 있음
- **범위** : 모든 URL은 URI이지만, 모든 URI가 URL인것은 아님
