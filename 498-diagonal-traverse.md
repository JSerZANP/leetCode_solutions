me explaining this on youtube: https://youtu.be/WPsWQJTTqfg

```js
/**
 * @param {number[][]} matrix
 * @return {number[]}
 */

// Time: O(m * n)
// Space: O(m * n)
var findDiagonalOrder = function(matrix) {
    const rows = matrix.length
    if (rows === 0) return []
  
    const cols = matrix[0].length
    const diagonals = new Array(rows + cols - 1).fill(0).map(_ => [])
    
    for (let i = 0; i < rows; i++) {
      for (let j = 0; j < cols; j++) {
        const key = i + j
        const num = matrix[i][j]
        if (key % 2 === 0) {
           diagonals[key].unshift(num)
        } else {
           diagonals[key].push(num)
        }
      }
    }
  
    // collect
    return diagonals.reduce((result, arr) => {
      result.push(...arr)
      return result
    }, [])
};
```
