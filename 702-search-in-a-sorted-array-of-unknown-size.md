```js
/**
 * // This is the ArrayReader's API interface.
 * // You should not implement it, or speculate about its implementation
 * function ArrayReader() {
 *
 *     @param {number} index
 *     @return {number}
 *     this.get = function(index) {
 *         ...
 *     };
 * };
 */

/**
 * @param {ArrayReader} reader
 * @param {number} target
 * @return {number}
 */
var search = function (reader, target) {
  let i = 0;
  let j = 10 ** 4 - 1;
  const overflow = 2 ** 31 - 1;
  while (i <= j) {
    const m = Math.floor((i + j) / 2);
    const mval = reader.get(m);
    if (mval === overflow) {
      j = m - 1;
    } else if (mval === target) {
      return m;
    } else if (mval < target) {
      i += 1;
    } else {
      j -= 1;
    }
  }
  return -1;
};
```
