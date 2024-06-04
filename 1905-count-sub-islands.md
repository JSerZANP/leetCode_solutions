```js
/**
 * @param {number[][]} grid1
 * @param {number[][]} grid2
 * @return {number}
 */
var countSubIslands = function (grid1, grid2) {
  const m = grid1.length;
  const n = grid1[0].length;
  // 1. determine the islands: BFS O(n^2) O(n^2)
  // 2. determine sub island: for all cells in an island, we check if they belong to the same island in grid1
  //   we need to store the island id for each cell, use a different grid (or maybe just the same grid)
  //   also we can get the flag during the BFS in grid

  const visitedGrid1 = new Array(m).fill(0).map((_) => new Array(n).fill(null));

  const directions = [
    [0, 1],
    [0, -1],
    [1, 0],
    [-1, 0],
  ];
  let islandId = 0;
  function walkGrid1(i, j) {
    if (visitedGrid1[i][j] != null || grid1[i][j] === 0) {
      return;
    }
    const queue = [[i, j]];
    while (queue.length > 0) {
      const head = queue.shift();
      if (visitedGrid1[head[0]][head[1]] != null) {
        continue;
      }
      visitedGrid1[head[0]][head[1]] = islandId;

      directions.forEach((direction) => {
        const next = [head[0] + direction[0], head[1] + direction[1]];
        if (
          next[0] >= 0 &&
          next[0] < m &&
          next[1] >= 0 &&
          next[1] < n &&
          grid1[next[0]][next[1]] === 1
        ) {
          queue.push(next);
        }
      });
    }
    islandId += 1;
  }

  for (let i = 0; i < m; i++) {
    for (j = 0; j < n; j++) {
      walkGrid1(i, j);
    }
  }

  // for grid2
  // TODO: we make the code resuable
  const visitedGrid2 = new Array(m)
    .fill(0)
    .map((_) => new Array(n).fill(false));

  let result = 0;
  function walkGrid2(i, j) {
    if (visitedGrid2[i][j] || grid2[i][j] === 0) {
      return;
    }
    const queue = [[i, j]];
    let islandIdInGrid1 = null;
    let isSubIsland = true;
    while (queue.length > 0) {
      const head = queue.shift();
      if (visitedGrid2[head[0]][head[1]]) {
        continue;
      }
      if (visitedGrid1[head[0]][head[1]] == null) {
        isSubIsland = false;
      } else {
        if (islandIdInGrid1 == null) {
          islandIdInGrid1 = visitedGrid1[head[0]][head[1]];
        } else if (islandIdInGrid1 != visitedGrid1[head[0]][head[1]]) {
          isSubIsland = false;
        }
      }

      visitedGrid2[head[0]][head[1]] = true;

      directions.forEach((direction) => {
        const next = [head[0] + direction[0], head[1] + direction[1]];
        if (
          next[0] >= 0 &&
          next[0] < m &&
          next[1] >= 0 &&
          next[1] < n &&
          grid2[next[0]][next[1]] === 1
        ) {
          queue.push(next);
        }
      });
    }
    if (isSubIsland) {
      result += 1;
    }
  }

  for (let i = 0; i < m; i++) {
    for (let j = 0; j < n; j++) {
      walkGrid2(i, j);
    }
  }

  return result;
};
```
