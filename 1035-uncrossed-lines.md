Youtube video explaining this: https://youtu.be/659LrloKNdw


```js
/**
 * @param {number[]} A
 * @param {number[]} B
 * @return {number}
 */
var maxUncrossedLines = function(A, B) {
    const results = new Array(A.length + 1);
    for (let i = 0; i < A.length + 1; i++) {
      results[i] = new Array(B.length + 1).fill(0);
    }
    for (let i = 1, totalA = A.length; i < totalA + 1; i++) {
      for (let j = 1, totalB = B.length; j < totalB + 1; j++) {
        if (A[i - 1] === B[j - 1]) {
          results[i][j] = results[i - 1][j - 1] + 1;
        } else {
          results[i][j] = Math.max(results[i][j - 1], results[i - 1][j]);
        }
      }
    }
    return results[A.length][B.length];
};
```
