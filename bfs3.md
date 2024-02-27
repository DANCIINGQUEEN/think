```js
const g = {
	A: ["B", "C"],
	B: ["A", "D"],
	C: ["A", "G", "H", "I"],
	D: ["B", "E", "F"],
	E: ["D"],
	F: ["D"],
	G: ["C"],
	H: ["C"],
	I: ["C", "J"],
	J: ["I"]
};
```

```js
const BFS = (g, start) => {
  let visited = []
  let needVisit = []
  needVisit.push(start)
  while(needVisit.length!==0){
    let node = needVisit.shift()
    if(!visited.included(node)){
      visited.push(node)
      needVisit = [...needVisit, ...g[node]]
    }
  }
  return visited
}
console.log(BFS(g, 'A'))
```

```js
const BFS = (g, start) => {
  let visited = new Set()
  let needVisit = []
  needVisit.push(start)
  while(needVisit.length!==0) {
    let node = needVisit.shift()
    if(!visited.has(node)){
      visited.add(node)
      needVisit.push(...graph[node])
    }
  }
  return visited
}
console.log(BFS(g, 'A'))
```
