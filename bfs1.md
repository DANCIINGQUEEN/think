
```javascript
class Graph {
  constructor() {
    this.adjacencyList = {};  // 그래프의 인접 리스트 초기화
  }

  addVertex(vertex) {
    if (!this.adjacencyList[vertex]) this.adjacencyList[vertex] = [];  // 새 정점 추가
  }

  addEdge(vertex1, vertex2) {
    this.adjacencyList[vertex1].push(vertex2);  // 첫 번째 정점에 두 번째 정점을 인접 정점으로 추가
    this.adjacencyList[vertex2].push(vertex1);  // 두 번째 정점에 첫 번째 정점을 인접 정점으로 추가
  }

  bfs(start) {
    const queue = [start];  // BFS 탐색을 위한 큐 초기화
    const result = [];  // 탐색 결과를 저장할 배열
    const visited = { [start]: true };  // 방문한 정점을 추적하는 객체
    let currentVertex;

    while (queue.length) {  // 큐에 노드가 남아있는 동안 반복
      currentVertex = queue.shift();  // 큐에서 정점을 하나 꺼냄
      result.push(currentVertex);  // 결과 배열에 현재 정점 추가

      this.adjacencyList[currentVertex].forEach(neighbor => {  // 현재 정점의 모든 이웃에 대해 반복
        if (!visited[neighbor]) {  // 아직 방문하지 않은 이웃일 경우
          visited[neighbor] = true;  // 방문한 것으로 표시
          queue.push(neighbor);  // 큐에 이웃 정점 추가
        }
      });
    }

    return result;  // 탐색 결과 반환
  }
}

// 그래프 생성 및 초기화 예제
const graph = new Graph();
graph.addVertex("A");
graph.addVertex("B");
graph.addVertex("C");
graph.addVertex("D");
graph.addEdge("A", "B");
graph.addEdge("A", "C");
graph.addEdge("B", "D");
graph.addEdge("C", "D");

// BFS 실행 및 결과 출력
console.log("BFS:", graph.bfs("A"));
```

이 코드는 그래프를 표현하고, BFS 알고리즘을 사용하여 그래프를 탐색하는 방법을 보여줍니다. 각 메소드와 구문에 주석을 달아 이해를 돕고 있습니다.

**후속 질문**:

**Q1:** 이 코드에서 `addVertex`와 `addEdge` 메소드의 목적은 무엇인가요?

**Q2:** 큐 대신 다른 자료 구조를 사용하면 어떤 결과가 발생할 수 있나요?

**Q3:** 이 BFS 구현에서 무방향 그래프를 사용한 이유는 무엇인가요?