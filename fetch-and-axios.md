# fetch와 axios의 차이점

1. 기본 제공 여부 및 환경 지원
   - fetch : JavaScript의 Fetch API는 모던 브라우저에 내장되어 있어 별도의 라이브러리 설치 없이 사용 가능
   - axiod : 별도로 설치해야되는 라이브러리. 자체적인 XHR(XMLHttpRequest)을 사용

2. 문법과 사용 용이성
   - fetch : 프로미스 기반의 API로 응답을 처리하기 위해 .json()과 같은 추가적인 메서드 호출해야됨
     ```js
     fetch('https://api.example.com/data')    // 응답 처리를 위한 추가 메스드 호출
        .then(response => {
          if (!response.ok) throw new Error('Network response was not ok');
          return response.json();
        })
        .then(data => console.log(data))
        .catch(error => console.error('Error:', error));
     ```
   - axios : 더 간결하고 직관적인 문법을 제공. JSON데이터를 자동으로 변환
     ```js
       axios.get('https://api.example.com/data')    //자동 JSON 변환
          .then(response => console.log(response.data))
          .catch(error => console.error('Error:', error));
     ```

3. 응답 상태 처리
   - fetch : HTTP 오류 상대(예 : 404, 500)가 발생해도 거부되지 않고 fullfilled상태의 프로미스 반환. 에러 처리를 위해 추가적인 로직 필요
   ```js
   fetch('https://api.example.com/data')  //응답 처리를 수동으로 확인
      .then(response => {
        if (!response.ok) throw new Error(`HTTP error! status: ${response.status}`);
        return response.json();
      })
      .then(data => console.log(data))
      .catch(error => console.error('Error:', error));
   ```
   - axios : HTTP오류 상태가 발생하면 자동으로 프로미스가 거부(reject)되고 , 이를 .catch()를 통해 쉽게 처리 가능
    ```js
    axios.get('https://api.example.com/data')  //HTTP 오류 상태 자동 거부
      .then(response => console.log(response.data))
      .catch(error => console.error('Error:', error));
    ```

4. 시간 초과 설정
   - fetch : 시간 초과 설정을 제공하지 않음. 커스텀 구현 필요
   ```js
   const fetchWithTimeout = (resource, options = {}) => {
      const { timeout = 8000 } = options;
      const controller = new AbortController();
      const id = setTimeout(() => controller.abort(), timeout);
      const response = fetch(resource, {
        ...options,
        signal: controller.signal  
      }).finally(() => clearTimeout(id));
      return response;
    };
   ```
   - axios : 시간 초과를 설정하는 기능을 내장하고 있어, 요청이 지정된 시간 안에 완료되지 않으면 실패
    ```js
    axios.get('https://api.example.com/data', { timeout: 8000 })
      .then(response => console.log(response.data))
      .catch(error => console.error('Error:', error));
    ```
  
5. 브라우저 호환성
   - fetch : 상대적으로 새로운 API이기 때문에 일부 오래된 브라우저에서는 지원하지 않을 수도 있음
   - axois : 더 넓은 브라우저 호환성 제공
  
6. 요청 취소
   - fetch : AbortController를 사용하여 구현
   ```js
    const controller = new AbortController();
    const signal = controller.signal;
    
    fetch('https://api.example.com/data', { signal })
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));
    
    // 요청 취소
    controller.abort();
   ```
   - axios : 요청 취소를 위한 API 제공
  ```js
    const CancelToken = axios.CancelToken;
    const source = CancelToken.source();
    
    axios.get('https://api.example.com/data', {
    cancelToken: source.token
    }).then(response => console.log(response.data))
    .catch(error => {
      if (axios.isCancel(error)) {
        console.log('Request canceled', error.message);
      } else {
        // 처리 오류
      }
    });
    
    // 요청 취소
    source.cancel('Operation canceled by the user.');
  ```

7. 진행 상태 모니터링
   - fetch : 없음
   - axios : HTTP 요청의 진행 상태를 추적할 수 있는 기능 제공
  ```js
    axios.get('https://api.example.com/data', {
      onDownloadProgress: progressEvent => {
        console.log('Download Progress:', progressEvent.loaded);
      },
      onUploadProgress: progressEvent => {
        console.log('Upload Progress:', progressEvent.loaded);
        }
      })
      .then(response => console.log(response.data))
      .catch(error => console.error('Error:', error));
  ```
   
