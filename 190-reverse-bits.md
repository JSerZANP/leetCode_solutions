```js
/**
 * @param {number} n - a positive integer
 * @return {number} - a positive integer
 */
var reverseBits = function (n) {
  const bits = [...n.toString(2).padStart(32, "0")];
  let i = 0;
  let j = bits.length - 1;
  while (i < j) {
    [bits[i], bits[j]] = [bits[j], bits[i]];
    i += 1;
    j -= 1;
  }
  return parseInt(bits.join(""), 2);
};
```
