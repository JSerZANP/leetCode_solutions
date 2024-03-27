```js
/**
 * @param {number[][]} logs
 * @param {number} k
 * @return {number[]}
 */
var findingUsersActiveMinutes = function (logs, k) {
  // [[0,5],[1,2],[0,2],[0,5],[1,3]]
  // 0 -> [5, 2]
  // 1 -> [2, 3]
  // Map<user, Set<minute>>
  const map = new Map();

  for (const [user, min] of logs) {
    if (!map.has(user)) {
      map.set(user, new Set());
    }
    map.get(user).add(min);
  }

  const result = new Array(k).fill(0);
  for (const [user, mins] of map) {
    result[mins.size - 1] += 1;
  }

  return result;
};
```
