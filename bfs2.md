
```javascript
function numIslands(grid) {
  let num = 0;

  // 격자의 모든 칸을 순회하며 상태를 출력하고, 섬의 개수를 계산
  for (let i = 0; i < grid.length; i++) {
    for (let j = 0; j < grid[0].length; j++) {
      // 현재 칸의 상태 출력
      process.stdout.write(grid[i][j] + " ");
      
      if (grid[i][j] === "1") {
        bfs(grid, i, j);
        num++;
      }
    }
    console.log(); // 현재 행이 끝나면 줄바꿈 출력
  }

  function bfs(grid, i, j) {
    let queue = [[i, j]];
    grid[i][j] = "0";

    while (queue.length) {
      let [x, y] = queue.shift();

      let directions = [[1, 0], [-1, 0], [0, 1], [0, -1]];
      for (let [dx, dy] of directions) {
        let newX = x + dx, newY = y + dy;

        if (newX >= 0 && newX < grid.length && newY >= 0 && newY < grid[0].length && grid[newX][newY] === "1") {
          queue.push([newX, newY]);
          grid[newX][newY] = "0";
        }
      }
    }
  }

  return num;
}

// 예시 격자 데이터
let grid = [
  ["1", "1", "0", "0", "0"],
  ["1", "1", "0", "0", "0"],
  ["0", "0", "1", "0", "0"],
  ["0", "0", "0", "1", "1"]
];

console.log("Number of islands:", numIslands(grid));
```
