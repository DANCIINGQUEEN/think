# Callback Hell
- 콜백 함수가 충접되어 코드의 가독성과 유지보수성이 떨어지는 현상
- 주로 비동기 작업을 처리할 때 발생


## Callback function
- 다른 함수에 인자로 전달되는 함수
- 호출되는 함수와 콜백 함수 2가지 함수 간의 상호작용을 통해 비동기적인 작업을 수행하거나 이벤트 처리, 코드를 재사용하는 등의 목적으로 사용
- 다른 함수가 실행된 후에 실행되도록 예약되어 사용됨
- 예 : 비동기적인 작업(네트워크 요청, 파일 읽기 등)이 끝나면 그 결과를 처리하기 위해 콜백 함수를 등록
  ```js
  function fetchDataFromServer(callback) {
    setTimeout(function () {
      const data = { name : 'Park' , age : 29 }
      callback(data)  //callback 함수 호출
    }, 1000)
  }

  function processData(data) {
    console.log('데이터 처리 완료 : ', data)
  }
  //fetchDataFromServer 함수의 인자로 processData 함수를 콜백으로 전달
  fetchdataFromServer(processData)
  ```
  - 위 코드에서 `fetchDataFromServer` 함수는 1초 후에 서버로부터 데이터를 가져옴
  - `processData` 함수가 콜백으로 전달되어, 데이터가 준비되면 `processData` 함수가 호출됨
 

```js
//Callback Hell by file system
const fs = require('fs')
//파일 읽기를 중첩된 콜백으로 처리하는 예시
fs.readFile('file1.txt', 'utf8', (e, data1) => {
  if (e) {
    console.error(e)
    return
  }
  console.log(data1)
  fs.readFile('file2.txt', 'utf8', (e, data2) => {
    if (e) {
      console.error(e)
      return
    }
    console.log(data2)
    fs.readFile('file3.txt', 'utf8', (e, data3) => {
      if (e) {
        console.error(e)
        return
      }
      console.lolg(data3)
      // 더 많은 중첩된 콜백...
    })
  })
})
```
- 위 코드는 세 개의 파일을 순차적으로 읽어야 할 때 발생하는 콜백 지옥의 예시
- 각 파일 읽기 작업이 완료된 후 다음 작업을 시작하려면 중첩된 콜백 구조가 필요

## Promise를 사용한 해결 방법
 - Promise를 사용하면 비동기 작업을 연속적으로 처리할 수 있음
```js
const fs = require('fs').promises

//Promise를 사용하여 파일을 순차적으로 읽는 예시
const readFile = (fileName) => {
  return fs.readFile(fileName, 'utf8')
}
readFile('file1.txt')
  .then(data1 => {
    console.log(data1)
    return readFile('file2.txt')
  })
  .then(data2 => {
    console.log(data2)
    return readFile('file3.txt')
  })
  .then(data3 => {
          console.log(data3);
  })
  .catch(err => {
      console.error(err);
  });
```
- 위 코드는 `Promise`를 사용하여 동일한 작업을 더 깔끔하게 처리함
- 각 파일을 읽은 후 다음 작업으로 넘어가는 과정이 `.then` 메서드 체인을 통해 이루어짐
- 오류 처리는 `.catch` 메서드를 사용하여 한 곳에서 처리할 수 있음

## Promise기반의 코드를 `async-await` 구문으로 개선
```js
const fs = require('fs').promises

//async 함수를 사용하여 파일을 순차적으로 읽는 예시
const readFileAsync = async () => {
  try {
    const data1 = await fs.readFile('file1.txt', 'utf8')
    console.log(data1)

    const data2 = await fs.readFile('file2.txt', 'utf8')
    console.log(data2)

    const data3 = await fs.readFile('file3.txt', 'utf8')
    console.log(data3)
  } catch (e) {
    console.error(e)
  }
}
readFileAsync()
```
- 위 코드에서 `readFileAsync` 함수는 `async`키워드를 사용해 선언됨
- 이는 함수 내에서 `await` 키워드를 사용할 수 있게 해줌. 해당 함수는 암묵적으로 Promise를 반환
- `await`키워드는 Promise가 완료될 때까지 함수의 실행을 일시적으로 중지하고, Promise가 완료되면 그 결과를 반환
- `try-catch` 블록은 비동기 작업에서 발생할 수 있는 오류를 잡아내는 역할
























