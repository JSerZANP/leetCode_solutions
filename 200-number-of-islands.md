## 1.

Here is a video explaining it: https://youtu.be/ImqyM7_R70E

```js
/**
 * @param {character[][]} grid
 * @return {number}
 */
var numIslands = function (grid) {
  // 1. step on one 1, start search for connected points (walk)
  // 2. use a 2d array to mark a pointed being walked on
  // 3. count the step 1

  const rows = grid.length;
  if (rows === 0) return 0;
  const cols = grid[0].length;

  const directions = [
    [0, 1],
    [0, -1],
    [1, 0],
    [-1, 0],
  ];

  const walked = new Array(rows)
    .fill(0)
    .map((_) => new Array(cols).fill(false));

  let result = 0;

  const walk = (row, col) => {
    result += 1;

    const stack = [[row, col]];
    walked[row][col] = true;

    while (stack.length > 0) {
      const top = stack.pop();
      for (let direction of directions) {
        const next = [top[0] + direction[0], top[1] + direction[1]];
        if (
          next[0] > -1 &&
          next[0] < rows &&
          next[1] > -1 &&
          next[1] < cols &&
          grid[next[0]][next[1]] === "1" &&
          !walked[next[0]][next[1]]
        ) {
          stack.push(next);
          walked[next[0]][next[1]] = true;
        }
      }
    }
  };

  for (let row = 0; row < rows; row++) {
    for (let col = 0; col < cols; col++) {
      // if it is land and not walked before
      if (grid[row][col] === "1" && !walked[row][col]) {
        walk(row, col);
      }
    }
  }

  return result;
};
```

## 2

```js
/**
 * @param {character[][]} grid
 * @return {number}
 */
var numIslands = function (grid) {
  const rows = grid.length;
  if (rows.length === 0) return 0;
  const cols = grid[0].length;
  if (cols.length === 0) return 0;
  // check each position
  // and use BFS to taint all 1s to 2
  // count

  // 0 - water
  // 1 - island
  // 2 - checked island

  function* nextValid(row, col) {
    const directions = [
      [0, 1],
      [0, -1],
      [1, 0],
      [-1, 0],
    ];
    for (const direction of directions) {
      const next = [row + direction[0], col + direction[1]];
      if (
        next[0] >= 0 &&
        next[1] >= 0 &&
        next[0] < rows &&
        next[1] < cols &&
        grid[next[0]][next[1]] === "1"
      ) {
        yield next;
      }
    }
  }

  function taint(row, col) {
    grid[row][col] = "2";
    for (const [nextRow, nextCol] of nextValid(row, col)) {
      taint(nextRow, nextCol);
    }
  }

  let count = 0;

  for (let i = 0; i < rows; i++) {
    for (let j = 0; j < cols; j++) {
      if (grid[i][j] === "1") {
        count += 1;
        taint(i, j);
      }
    }
  }

  return count;
};
```

Another try

```js
/**
 * @param {character[][]} grid
 * @return {number}
 */
var numIslands = function (grid) {
  const rows = grid.length;
  const cols = grid[0].length;
  // start from a cell of 1
  // and tain all the cells into 2
  // for each round increase the island count
  // tain => BFS
  let count = 0;

  const directions = [
    [0, 1],
    [0, -1],
    [1, 0],
    [-1, 0],
  ];

  grid.forEach((row, i) => {
    row.forEach((num, j) => {
      if (num === "1") {
        taint(i, j);
      }
    });
  });

  function taint(i, j) {
    count += 1;

    const queue = [[i, j]];
    while (queue.length > 0) {
      let size = queue.length;
      while (size > 0) {
        const head = queue.shift();
        if (grid[head[0]][head[1]] === "1") {
          grid[head[0]][head[1]] = 2;

          for (const direction of directions) {
            const next = [head[0] + direction[0], head[1] + direction[1]];
            if (
              next[0] >= 0 &&
              next[0] < rows &&
              next[1] >= 0 &&
              next[1] < cols &&
              grid[next[0]][next[1]] === "1"
            ) {
              queue.push(next);
            }
          }
        }
        size -= 1;
      }
    }
  }

  return count;
};
```
