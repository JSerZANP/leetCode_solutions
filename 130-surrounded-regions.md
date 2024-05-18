```js
/**
 * @param {character[][]} board
 * @return {void} Do not return anything, modify board in-place instead.
 */
var solve = function (board) {
  const rows = board.length;
  const cols = board[0].length;

  const visited = new Array(rows)
    .fill(0)
    .map((_) => new Array(cols).fill(false));

  const directions = [
    [0, 1],
    [0, -1],
    [1, 0],
    [-1, 0],
  ];

  const tryToFlip = (i, j) => {
    // itself might be at border
    if (i == 0 || j == 0 || i === rows - 1 || j === cols - 1) {
      visited[i][j] = true;
      return;
    }

    const queue = [[i, j]];
    const candidates = [];
    let isAbleToFlip = true;
    while (queue.length > 0) {
      const head = queue.shift();
      if (
        head[0] == 0 ||
        head[1] == 0 ||
        head[0] === rows - 1 ||
        head[1] === cols - 1
      ) {
        isAbleToFlip = false;
      }
      if (!visited[head[0]][head[1]]) {
        visited[head[0]][head[1]] = true;
        candidates.push(head);

        for (const direction of directions) {
          const next = [head[0] + direction[0], head[1] + direction[1]];
          // for all connected cells
          if (
            next[0] >= 0 &&
            next[0] < rows &&
            next[1] >= 0 &&
            next[1] < cols &&
            board[next[0]][next[1]] === "O"
          ) {
            if (
              next[0] === 0 ||
              next[0] === rows - 1 ||
              next[1] === 0 ||
              next[1] === cols - 1
            ) {
              isAbleToFlip = false;
            }
            if (!visited[next[0]][next[1]]) {
              queue.push(next);
            }
          }
        }
      }
    }
    if (isAbleToFlip) {
      candidates.forEach((candidate) => {
        board[candidate[0]][candidate[1]] = "X";
      });
    }
  };

  for (let i = 0; i < rows; i++) {
    for (let j = 0; j < cols; j++) {
      if (board[i][j] === "O" && !visited[i][j]) {
        tryToFlip(i, j);
      }
    }
  }
};
```
