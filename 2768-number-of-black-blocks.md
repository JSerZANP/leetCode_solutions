Naive solution: memory bloat.

```js
/**
 * @param {number} m
 * @param {number} n
 * @param {number[][]} coordinates
 * @return {number[]}
 */
var countBlackBlocks = function (m, n, coordinates) {
  // for m x n, how many blocks?
  // (m - 1) * (n - 1) blocks
  // to count the black cells : O(4)
  // O((m - 1) * (n - 1) * 4 * 5)

  // if there is only one black cell,
  // it seems more efficient to only focus on the black cell to see how many blocks it disables?
  // when we place a cell, we can actually update the black cell count in O(4)
  // then we can just check all blocks
  // O((m - 1) * (n - 1) + O(4 * k))

  // use the top-left coordinate to indicate the blocks
  const blocks = new Array(m).fill(0).map((_) => new Array(n).fill(0));
  for (const coord of coordinates) {
    const [i, j] = coord;
    if (i < m - 1 && j < n - 1) {
      blocks[i][j] += 1;
    }
    if (i - 1 >= 0 && j < n - 1) {
      blocks[i - 1][j] += 1;
    }
    if (i - 1 >= 0 && j - 1 >= 0) {
      blocks[i - 1][j - 1] += 1;
    }
    if (i < m - 1 && j - 1 >= 0) {
      blocks[i][j - 1] += 1;
    }
  }

  const result = new Array(5).fill(0);
  for (let i = 0; i < m - 1; i++) {
    for (let j = 0; j < n - 1; j++) {
      result[blocks[i][j]] += 1;
    }
  }
  return result;
};
```

Maybe the allocation of all blocks are too much, we can just do it lazily with map.

Also we don't need to do the final traversal, because every time we check,
we are basically moving a block from i black blocks to i + 1

```js
var countBlackBlocks = function (m, n, coordinates) {
  // for m x n, how many blocks?
  // (m - 1) * (n - 1) blocks
  // to count the black cells : O(4)
  // O((m - 1) * (n - 1) * 4 * 5)

  // if there is only one black cell,
  // it seems more efficient to only focus on the black cell to see how many blocks it disables?
  // when we place a cell, we can actually update the black cell count in O(4)
  // then we can just check all blocks
  // O((m - 1) * (n - 1) + O(4 * k))

  // use the top-left coordinate to indicate the blocks
  const blocks = new Map();
  const result = new Array(5).fill(0);
  result[0] = (m - 1) * (n - 1);
  for (const coord of coordinates) {
    const [i, j] = coord;
    if (i < m - 1 && j < n - 1) {
      const prev = blocks.get(`${i}_${j}`) ?? 0;
      result[prev] -= 1;
      result[prev + 1] += 1;
      blocks.set(`${i}_${j}`, prev + 1);
    }
    if (i - 1 >= 0 && j < n - 1) {
      const prev = blocks.get(`${i - 1}_${j}`) ?? 0;
      result[prev] -= 1;
      result[prev + 1] += 1;
      blocks.set(`${i - 1}_${j}`, prev + 1);
    }
    if (i - 1 >= 0 && j - 1 >= 0) {
      const prev = blocks.get(`${i - 1}_${j - 1}`) ?? 0;
      result[prev] -= 1;
      result[prev + 1] += 1;
      blocks.set(`${i - 1}_${j - 1}`, prev + 1);
    }
    if (i < m - 1 && j - 1 >= 0) {
      const prev = blocks.get(`${i}_${j - 1}`) ?? 0;
      result[prev] -= 1;
      result[prev + 1] += 1;
      blocks.set(`${i}_${j - 1}`, prev + 1);
    }
  }

  return result;
};
```
