Here is my video explaining it: https://youtu.be/qlLqOIDH-Ow

```js
/**
 * @param {number[]} A
 * @return {boolean}
 */

// Time: O(n)
// Space: O(1)
var isMonotonic = function(A) {
  let isAcending = true
  let isDecending = true
  
  for (let i = 1; i < A.length; i++) {
    if (A[i] > A[i - 1]) {
      isDecending = false
    }
    
    if (A[i] < A[i - 1]) {
      isAcending  = false
    }
  }
  
  return isAcending || isDecending
};
```
