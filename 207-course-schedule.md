```js
/**
 * @param {number} numCourses
 * @param {number[][]} prerequisites
 * @return {boolean}
 */
var canFinish = function (numCourses, prerequisites) {
  // a -> b
  // b => c

  // Map<number, Set<number>>
  // the problem is to check for each course
  // if there is a circle

  // DFS
  // use a Set visited to track the visited node
  // there might be duplicate checks, memo the check result
  const map = new Map();
  for (const [from, to] of prerequisites) {
    if (map.has(from)) {
      map.get(from).add(to);
    } else {
      map.set(from, new Set([to]));
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
      return false;
    }
  }
  return true;
};
```
