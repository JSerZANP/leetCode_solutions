```js
/**
 * @param {string} s
 * @return {number}
 */
var minimumChairs = function (s) {
  let count = 0;
  let max = 0;
  for (const char of s) {
    if (char === "E") {
      count += 1;
      max = Math.max(max, count);
    } else {
      count -= 1;
    }
  }
  return max;
};
```
