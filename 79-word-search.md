## 1

A video explaining this: https://youtu.be/IifOOxXVanQ

```js
/**
 * @param {character[][]} board
 * @param {string} word
 * @return {boolean}
 */

const directions = [
  [0, 1], // right,
  [0, -1], // left,
  [1, 0], // down
  [-1, 0], // up
];

var exist = function (board, word) {
  // a map to keep track of the usage
  const isUsed = board.map((row) => row.map((_) => false));

  const target = word.split("");
  const current = [];

  let isFound = false;

  const walk = (i, j) => {
    // out of board
    if (i < 0 || i > board.length - 1) return false;
    if (j < 0 || j > board[0].length - 1) return false;

    // used
    if (isUsed[i][j]) return false;

    // check if the letter is what we want
    if (board[i][j] === target[0]) {
      current.push(target.shift());
      isUsed[i][j] = true;

      // ending condition
      if (target.length === 0) {
        isFound = true;
        return true;
      }

      // continue the next walk in for directions
      for (let direction of directions) {
        const [newI, newJ] = [i + direction[0], j + direction[1]];
        // find the match
        if (walk(newI, newJ)) {
          return true;
        }
      }

      // back tracking
      target.unshift(current.pop());
      isUsed[i][j] = false;
    }

    return false;
  };

  for (let i = 0; i < board.length; i++) {
    for (let j = 0; j < board[0].length; j++) {
      if (walk(i, j)) {
        return true;
      }
    }
  }

  return false;
};
```

## 2.

```js
var exist = function (board, word) {
  if (board.length === 0) return false;
  if (board[0].length === 0) return false;
  // start from each cell
  // try to match every word
  // exist(board, word, x, y)

  // check every cell
  // exist(board, ABCCED, 0, 0)
  // exist(board, BCCED, 0, 1), exist(board, BCCED, 1, 0)
  // stop if we canot match any longer
  // path is `x_y`
  const directions = [
    [0, 1],
    [0, -1],
    [1, 0],
    [-1, 0],
  ];
  function existFrom(x, y, word, path = new Set()) {
    if (board[x][y] !== word[0]) {
      return false;
    }

    if (word.length === 1) {
      return true;
    }

    const position = `${x}_${y}`;

    path.add(position);

    for (const direction of directions) {
      const sibling = [x + direction[0], y + direction[1]];
      if (
        isValid(sibling[0], sibling[1], path, board) &&
        existFrom(sibling[0], sibling[1], word.slice(1), path)
      ) {
        return true;
      }
    }

    path.delete(position);

    return false;
  }
  function isValid(x, y, path, board) {
    if (path.has(`${x}_${y}`)) {
      return false;
    }
    return x >= 0 && y >= 0 && x < board.length && y < board[0].length;
  }

  for (let i = 0; i < board.length; i++) {
    for (let j = 0; j < board[0].length; j++) {
      if (existFrom(i, j, word)) {
        return true;
      }
    }
  }
  return false;
};
```
