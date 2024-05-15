A video explaining this: https://youtu.be/-famaCHwEyI

```js
/**
 * @param {number[][]} matrix
 * @return {void} Do not return anything, modify matrix in-place instead.
 */
var rotate = function (matrix) {
  let depth = 0;
  const maxDepth = Math.floor(matrix.length / 2);

  while (depth < maxDepth) {
    const length = matrix.length - depth * 2;
    const left = depth;
    const top = depth;

    for (let i = 0; i < length - 1; i++) {
      let first = matrix[top][left + i];
      let next = matrix[top + i][left + length - 1];

      matrix[top + i][left + length - 1] = first;

      first = next;
      next = matrix[top + length - 1][left + length - 1 - i];

      matrix[top + length - 1][left + length - 1 - i] = first;

      first = next;
      next = matrix[top + length - 1 - i][left];

      matrix[top + length - 1 - i][left] = first;

      matrix[top][left + i] = next;
    }

    depth += 1;
  }
};
```

Another try

```js
/**
 * @param {number[][]} matrix
 * @return {void} Do not return anything, modify matrix in-place instead.
 */
var rotate = function (matrix) {
  // only need a map between prev coordinate to the new one
  // ith row -> n - 1 -i th col
  // jth col -> jth row

  // since we cannot allocate a new matrix
  // move an item to the next position and move that item

  // roate layer by layer
  // there are Math.floor(n / 2) layer

  // for each layer we rotate items on the first row except that last one
  const n = matrix.length; // 3
  const layers = Math.ceil(n / 2); // 2
  for (let i = 0; i < layers; i++) {
    // rotate each layer
    const size = n - i * 2; // 3

    for (let j = i; j < i + size - 1; j++) {
      let current = matrix[i][j]; // 3
      let pos = [i, j]; // [2, 0]
      do {
        let relativePos = [pos[0] - i, pos[1] - i];
        relativePos = [relativePos[1], size - 1 - relativePos[0]];
        pos = [i + relativePos[0], i + relativePos[1]];
        const temp = matrix[pos[0]][pos[1]];
        matrix[pos[0]][pos[1]] = current;
        current = temp;
      } while (!(pos[0] === i && pos[1] === j));
    }
  }
};
```
