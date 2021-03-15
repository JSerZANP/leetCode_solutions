here is my video to explain this: https://youtu.be/CNZK3o9vZg8


```js
/**
 * @param {number[]} A
 * @param {number} L
 * @param {number} M
 * @return {number}
 */

// Time: O(n)
// space: O(n)
var maxSumTwoNoOverlap = function(A, L, M) {
    // for 1 sub array
    // sliding window to get max sum  O(n)
  
    // 1. loop through A for size L
    //     1. get max of M at the head
    //     2. get max of M at the rare (this needs to be pre calculated)
  
    const maxMStartFrom = []
    
    let currentMax = -Infinity
    let currentSum = 0
    for (let i = A.length - 1; i >= 0; i--) {
      currentSum += A[i]
      
      if (i < A.length - M) {
        currentSum -= A[i + M]
      }
      
      if (i <= A.length - M) {
        currentMax = Math.max(currentMax, currentSum)
        maxMStartFrom[i] = currentMax
      }
    }
  
    // process L
    const maxMEndAt = []
    let currentSumL = 0
    let currentSumM = 0
    let currentMaxM = -Infinity
    
    
    let maxSum = -Infinity
    
    for (let i = 0; i < A.length; i++) {
      currentSumM += A[i]
      if (i > M - 1) {
        currentSumM -= A[i - M]
      }
      
      if (i >= M - 1) {
        currentMaxM = Math.max(currentMaxM, currentSumM)
        maxMEndAt[i] = currentMaxM
      }
      
      // calculate the sum for L
      currentSumL += A[i]
      if (i > L - 1) {
        currentSumL -= A[i - L]
      }
      
      if (i >= L - 1) {
        // update hte final maxSum
        const maxSumMFromLeft = i - L < M - 1 ? 0 : maxMEndAt[i - L]
        const maxSumMFromRight = i + 1 + M - 1 < A.length ? maxMStartFrom[i + 1] : 0
        maxSum = Math.max(
          maxSum, 
          currentSumL + Math.max(maxSumMFromLeft, maxSumMFromRight)
          )
      }
      
    }
  
    return maxSum
};

```
