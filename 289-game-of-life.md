```js
/**
 * @param {number[][]} board
 * @return {void} Do not return anything, modify board in-place instead.
 */
var gameOfLife = function (board) {
  // 01 => 0 -> 1
  // 11 => 1 -> 1
  // 10 => 1 -> 0
  // 00 => 0 -> 0

  let rows = board.length;
  let cols = board[0].length;
  for (let i = 0; i < rows; i++) {
    for (let j = 0; j < cols; j++) {
      const actualVal = board[i][j] && 1;
      const liveNeighborsCount = getLiveNeighborsCount(board, i, j);
      if (actualVal === 1 && liveNeighborsCount < 2) {
        // do nothing
      }
      if (
        actualVal === 1 &&
        liveNeighborsCount >= 2 &&
        liveNeighborsCount <= 3
      ) {
        board[i][j] = board[i][j] + 2;
      }
      if (actualVal === 1 && liveNeighborsCount > 3) {
        // do nothing
      }

      if (actualVal === 0 && liveNeighborsCount === 3) {
        board[i][j] = board[i][j] + 2;
      }
    }
  }
  for (let i = 0; i < rows; i++) {
    for (let j = 0; j < cols; j++) {
      board[i][j] = board[i][j] >> 1;
    }
  }
};

function getLiveNeighborsCount(board, i, j) {
  let count = 0;
  [-1, 0, 1].forEach((row) => {
    [-1, 0, 1].forEach((col) => {
      if (row === 0 && col === 0) return;
      if (
        i + row >= 0 &&
        i + row < board.length &&
        j + col >= 0 &&
        j + col < board[0].length &&
        board[i + row][j + col] % 2 === 1
      ) {
        count += 1;
      }
    });
  });
  return count;
}
```
