```js
/**
 * @param {number} numCourses
 * @param {number[][]} prerequisites
 * @return {number[]}
 */
var findOrder = function (numCourses, prerequisites) {
  // following 207
  // when we find that there is no circle
  // it is a tree-like structure
  // we can just with the leaf nodes that don't have pre-requisities
  // that means we need to also track the depth of each node

  // height: max depth from the leaf node.
  // leaf node: no prerequisities

  // in this approach, we need to sort the node by height?

  // what if we don't need to?

  // we can just DFS from the existing tree and reverse the result?
  // no we still need the depth

  const map = new Map();
  const reverseMap = new Map();
  const leafNodes = new Set();
  for (let i = 0; i < numCourses; i++) {
    leafNodes.add(i);
  }
  for (const [from, to] of prerequisites) {
    leafNodes.delete(from);
    if (map.has(from)) {
      map.get(from).add(to);
    } else {
      map.set(from, new Set([to]));
    }

    if (reverseMap.has(to)) {
      reverseMap.get(to).add(from);
    } else {
      reverseMap.set(to, new Set([from]));
    }
  }
  const cache = new Map();

  function hasCircle(node, visited = new Set()) {
    if (cache.has(node)) {
      return cache.get(node);
    }

    if (visited.has(node)) {
      cache.set(node, true);
      return true;
    }

    const pres = map.get(node) ?? new Set();
    if (pres.size === 0) {
      cache.set(node, false);
      return false;
    }

    visited.add(node);
    for (const pre of pres) {
      if (hasCircle(pre, visited)) {
        cache.set(node, true);
        return true;
      }
    }
    visited.delete(node);
    cache.set(node, false);
    return false;
  }

  for (const [from, to] of map.entries()) {
    if (hasCircle(from)) {
      return [];
    }
  }

  const heightMap = new Map();
  for (let i = 0; i < numCourses; i++) {
    heightMap.set(i, 0);
  }
  const walk = (node, height = 0) => {
    heightMap.set(node, Math.max(heightMap.get(node) ?? 0, height));
    const nextNodes = reverseMap.get(node) ?? new Set();
    for (const nextNode of nextNodes) {
      walk(nextNode, height + 1);
    }
  };
  leafNodes.forEach((node) => walk(node, 0));
  const result = [];
  const entries = [...heightMap.entries()].sort((a, b) => a[1] - b[1]);
  return entries.map((item) => item[0]);
};
```
