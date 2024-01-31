
```javascript
class Graph {
  constructor() {
    this.adjacencyList = {};  // 그래프의 인접 리스트 초기화
  }

  addVertex(vertex) {
    if (!this.adjacencyList[vertex]) this.adjacencyList[vertex] = [];  // 새 정점 추가
    return this;
  }

  addEdge(vertex1, vertex2) {
    this.adjacencyList[vertex1].push(vertex2);  // 첫 번째 정점에 두 번째 정점을 인접 정점으로 추가
    this.adjacencyList[vertex2].push(vertex1);  // 두 번째 정점에 첫 번째 정점을 인접 정점으로 추가
    return this;
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
graph.addVertex("A").addVertex("B").addVertex("C").addVertex("D").addEdge("A", "B").addEdge("A", "C").addEdge("B", "D").addEdge("C", "D");
// BFS 실행 및 결과 출력
console.log("BFS:", graph.bfs("A"));
```


