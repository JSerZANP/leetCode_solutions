```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var singleNumber = function (nums) {
  let visited = new Set();
  let candidates = new Set();
  for (const num of nums) {
    if (visited.has(num)) {
      candidates.delete(num);
    } else {
      candidates.add(num);
      visited.add(num);
    }
  }
  return candidates.values().next().value;
};
```
