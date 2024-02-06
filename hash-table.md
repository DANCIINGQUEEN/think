# Hash Table
- 해시테이블은 키를 사용하여 데이터를 저장하는 데이터 구조
- 해시 함수를 사용하여 키를 배열 인덱스로 변환
- 인덱스를 사용하여 데이터를 배열에 저장하거나 검색

## 장점
  - 효율적인 테이터 검색과 접근 : 평균적으로 O(1)의 시간 복잡도를 가짐
  - 키에 대한 직접 접근 : 키를 사용하여 데이터를 빠르게 검색
## 단점
  - 충돌 처리 복잡성 : 충돌이 빈번하게 발생하면 성능이 저하됨
  - 메모리 사용 : 추가적인 메모리 공간이 필요할 수 있으며, 특히 동적 리사이징을 할 때는 메모리 사용량이 급증할 수 있음
  ```js
  claass HashTable {
    constructor(size=42) {
      this.buckets = new Array(size)
      this.size = size
    }

    hash(key) {
      let hash = 0
      for (let i=0; i<key.length; i++) {
        hash = (hash + key.charCodeAt(i) * i) % this.size
      }
      return hash
    }

    set(key, value) {
      let index = this.hash(key)
      if (!this.buckets[index]) {
        this.buckets[index] = []
      }
      this.buckets[index].push([key, value])
      return index
    }
  }


  const myHashTable = new HashTable()
  myHashTable.set('name', 'Park')
  myHashTable.set('age', '29')
  console.log(myHashTable.get('name'))  // print : Park
  console.log(myHashTable.get('age'))    // print : 29
  ```

  - HashTable 클래스 : 해시테이블을 구현하는 클래스
    - `constructor` : 기본크기(기본값 42)의 배열(`buckets`)을 생성
    - `hash` : 키를 배열 인덱스로 변환하는 해시함수. 간단한 문자열 해시 함수로, 각 문자의 코드를 이용
    - `set` :키와 값을 해시테이블에 저장. 해시 함수를 사용하여 키에 해당하는 인덱스를 찾고, 해당 위치에 키와 값을 저장
    - `get` : 키에 해당하는 값을 해시테이블에서 검색. 해시 함수로 인덱스를 찾고, 해당 버킷에서 키와 일치하는 값을 찾아 반환
   
    
