```js
/**
 * @param {number} n
 * @return {number}
 */
var hammingWeight = function (n) {
  // keep getting the bits
  let count = 0;
  while (n > 0) {
    const lastBit = n % 2;
    if (lastBit > 0) {
      count += 1;
    }
    n = (n - lastBit) / 2;
  }
  return count;
};
```
