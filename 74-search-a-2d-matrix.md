Here is a video explaining this: https://youtu.be/4UUIbkwkzGQ


```js
/**
 * @param {number[][]} matrix
 * @param {number} target
 * @return {boolean}
 */

// binary search 2 round
// logM + logN  = logMN
// constant O(1)
var searchMatrix = function(matrix, target) {
    if (matrix.length === 0) return false
  
    let i = 0
    let j = matrix.length - 1
    
    while (i < j) {
      const middle = Math.ceil((i + j) / 2) // choose the ceiling, throw right half
      const num = matrix[middle][0]
      
      if (num === target) {
        return true
      }  else if (num < target) {
        i = middle
      } else { 
        j = middle - 1
      }
    }
  
    // when i meets j, row is targeted
    let k = 0
    let l = matrix[i].length - 1
    
    while (k <= l) {
      const middle = Math.ceil((k + l) / 2)
      const num = matrix[i][middle]
      if (num === target) {
        return true
      } else if (num < target) {
        k = middle + 1
      } else {
        l = middle - 1
      }
    }
  
    return false
};
```
