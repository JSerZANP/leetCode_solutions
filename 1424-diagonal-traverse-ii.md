Me explaining this on youtube: https://youtu.be/4I9TFHyFUNY

```js
/**
 * @param {number[][]} nums
 * @return {number[]}
 */


// Time: O(element count) + O(diagonal count) => worst O(m n)
// Space: worst O(m n)
var findDiagonalOrder = function(matrix) {
    const rows = matrix.length
    const cols = matrix[0].length
    const diagonals = []
    
    for (let i = 0; i < rows; i++) {
      for (let j = 0; j < matrix[i].length; j++) {
        const num = matrix[i][j]
        if (num === undefined) break
        const key = i + j
        if (diagonals[key]) {
            diagonals[key].unshift(num)
        } else {
           diagonals[key] = [num]
        }
      }
    }
  
    const result = []
    for (let diagonal of diagonals) {
      if (diagonal) {
        result.push(...diagonal)
      }
    }
    return result
};
```
