```js
/**
 * Forward declaration of guess API.
 * @param {number} num   your guess
 * @return 	     -1 if num is higher than the picked number
 *			      1 if num is lower than the picked number
 *               otherwise return 0
 * var guess = function(num) {}
 */

/**
 * @param {number} n
 * @return {number}
 */
var guessNumber = function (n) {
  let i = 1;
  let j = n;
  while (i <= j) {
    const m = Math.floor((i + j) / 2);
    const guessResult = guess(m);
    if (guessResult === 0) {
      return m;
    } else if (guessResult < 0) {
      j = m - 1;
    } else {
      i = m + 1;
    }
  }
  // should not come here
  throw new Error("there should be a result");
};
```
