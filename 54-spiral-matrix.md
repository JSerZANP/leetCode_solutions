Youtube video explaining this: https://youtu.be/95zEFgS4WSo

```js
/**
 * @param {number[][]} matrix
 * @return {number[]}
 */
var spiralOrder = function (matrix) {
  if (matrix.length === 0 || matrix[0].length === 0) return [];

  const directions = [
    [0, 1],
    [1, 0],
    [0, -1],
    [-1, 0],
  ];

  let currentDirectionIndex = 0;

  const turnRight = () => {
    currentDirectionIndex = (currentDirectionIndex + 1) % directions.length;
  };

  const result = [];

  let i = 0;
  let j = 0;
  const total = matrix.length * matrix[0].length;

  while (result.length < total) {
    result.push(matrix[i][j]);
    matrix[i][j] = null;

    // check if we need to turn right
    const nextPossible = [
      i + directions[currentDirectionIndex][0],
      j + directions[currentDirectionIndex][1],
    ];

    // if it is overflowed, or it is traversed, turn right
    if (
      nextPossible[0] < 0 ||
      nextPossible[0] >= matrix.length ||
      nextPossible[1] < 0 ||
      nextPossible[1] >= matrix[0].length ||
      matrix[nextPossible[0]][nextPossible[1]] === null
    ) {
      turnRight();
    }

    i += directions[currentDirectionIndex][0];
    j += directions[currentDirectionIndex][1];
  }

  return result;
};
```

Another try

```js
/**
 * @param {number[][]} matrix
 * @return {number[]}
 */
var spiralOrder = function (matrix) {
  const rows = matrix.length;
  if (rows === 0) return [];
  const cols = matrix[0].length;
  if (cols === 0) return [];
  // direction
  // turn right when cannot moveforward

  let direction = [0, 1];

  let pos = [0, -1];

  const visited = new Array(rows)
    .fill(0)
    .map((_) => new Array(cols).fill(false));

  const result = [];
  let turnedRightCount = 0;

  function turnRight() {
    turnedRightCount += 1;
    direction = [direction[1], -direction[0]];
  }

  while (true) {
    // for each move
    // check if next position can be walked upon
    const next = [pos[0] + direction[0], pos[1] + direction[1]];
    if (
      next[0] >= 0 &&
      next[0] < rows &&
      next[1] >= 0 &&
      next[1] < cols &&
      !visited[next[0]][next[1]]
    ) {
      pos = next;
      result.push(matrix[pos[0]][pos[1]]);
      visited[pos[0]][pos[1]] = true;
      turnedRightCount = 0;
    } else {
      if (turnedRightCount > 0) {
        break;
      }
      // turn right once
      turnRight();
    }
  }
  return result;
};
```
