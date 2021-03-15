Youtube video explaining this: https://youtu.be/VAEqcS77iLo


```js
/**
 * @param {number[]} A
 * @param {number} K
 * @return {number}
 */
var maxSumAfterPartitioning = function(A, K) {
    const result = [A[0]]
    for (let i = 1; i < A.length; i++) {
      let temp = A[i] + result[i - 1] // [ A[i] ]
      if (i > 0) {
          let maxItem = A[i]
          for (let j = i - 1; j >= 0 && j > i - K; j--) {
            maxItem = Math.max(maxItem, A[j])
            temp = Math.max(temp, (i - j + 1) * maxItem + (j > 0 ? result[j - 1] : 0))
          }
      }
      result.push(temp)
    }
    return result[A.length - 1]
};
```
