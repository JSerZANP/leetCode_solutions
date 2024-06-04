```js
/**
 * @param {number} n
 * @param {number[][]} edges
 * @return {number}
 */
var countComponents = function (n, edges) {
  // DFS or BFS, count, visited
  const edgeMap = new Map();
  for (const [from, to] of edges) {
    if (edgeMap.has(from)) {
      edgeMap.get(from).add(to);
    } else {
      edgeMap.set(from, new Set([to]));
    }

    if (edgeMap.has(to)) {
      edgeMap.get(to).add(from);
    } else {
      edgeMap.set(to, new Set([from]));
    }
  }

  let count = 0;
  const visited = new Set();
  const walk = (i) => {
    if (visited.has(i)) {
      return;
    }

    visited.add(i);
    if (edgeMap.has(i)) {
      for (const to of edgeMap.get(i)) {
        walk(to);
      }
    }
  };

  for (let i = 0; i < n; i++) {
    if (!visited.has(i)) {
      count += 1;
      walk(i);
    }
  }
  return count;
};
```
