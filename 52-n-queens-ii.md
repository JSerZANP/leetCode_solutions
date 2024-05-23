Youtube video explaining this: https://youtu.be/gcqGtHZx3-w

```js
/**
 * @param {number} n
 * @return {number}
 */
var totalNQueens = function (n) {
  let result = 0;
  const board = Array(n)
    .fill(0)
    .map((_) => Array(n).fill("."));

  const colsUsed = Array(n).fill(false);
  const diago135Used = Array(n * 2 - 1).fill(false);
  const diago45Used = Array(n * 2 - 1).fill(false);

  const put = (i, j) => {
    const indexOfDiago135 = i + n - j - 1;
    const indexOfDiago45 = i + j;
    // if not available
    if (
      colsUsed[j] ||
      diago135Used[indexOfDiago135] ||
      diago45Used[indexOfDiago45]
    ) {
      return;
    }

    // if possible, put Queen in
    board[i][j] = "Q";
    colsUsed[j] = true;
    diago135Used[indexOfDiago135] = true;
    diago45Used[indexOfDiago45] = true;

    // last Queen is put
    if (i === n - 1) {
      result += 1;
    } else {
      for (let k = 0; k < n; k++) {
        put(i + 1, k);
      }
    }

    board[i][j] = ".";
    colsUsed[j] = false;
    diago135Used[indexOfDiago135] = false;
    diago45Used[indexOfDiago45] = false;
  };

  for (let k = 0; k < n; k++) {
    put(0, k);
  }

  return result;
};
```

Another try in 2024

```js
/**
 * @param {number} n
 * @return {number}
 */
var totalNQueens = function (n) {
  // since queen can move in any direction, horizontal, vertical or diagonal
  // each queen must be place in each row and col
  // regarding the diagonal, also use a row to keep track of the usage
  const isColUsed = new Array(n).fill(false);
  const isDiagonalUsed45 = new Array(2 * n - 1).fill(false);
  const isDiagonalUsed135 = new Array(2 * n - 1).fill(false);

  // place the ith queen, it must be in ith row
  // so just loop through the cols
  let count = 0;
  const place = (i) => {
    if (i >= n) {
      count += 1;
      return;
    }
    for (let j = 0; j < n; j++) {
      const indexDiagonal45 = i + j;
      const indexDiagonal135 = n - 1 - j + i;
      if (
        !isColUsed[j] &&
        !isDiagonalUsed45[indexDiagonal45] &&
        !isDiagonalUsed135[indexDiagonal135]
      ) {
        isColUsed[j] = true;
        isDiagonalUsed45[indexDiagonal45] = true;
        isDiagonalUsed135[indexDiagonal135] = true;
        place(i + 1);
        isColUsed[j] = false;
        isDiagonalUsed45[indexDiagonal45] = false;
        isDiagonalUsed135[indexDiagonal135] = false;
      }
    }
  };

  place(0);
  return count;
};
```
