Here is a video explaining: https://www.youtube.com/watch?v=rvrbBIUBsKs

```js
/**
 * @param {number[][]} mat
 * @return {number}
 */

// Time: O(2mn) O(mn)
// Space: O(m + n)
var numSpecial = function(mat) {
  const rows = mat.length
  const cols = mat[0].length
  
  const count1Rows = new Array(rows).fill(0)
  const count1Cols = new Array(cols).fill(0)
  
  for (let row = 0; row < rows; row++) {
    for (let col = 0; col < cols; col++) {
      if (mat[row][col] === 1) {
        count1Rows[row] += 1
        count1Cols[col] += 1
      }
    }
  }
  
  let result = 0
  for (let row = 0; row < rows; row++) {
    for (let col = 0; col < cols; col++) {
      if (mat[row][col] === 1 && count1Rows[row] === 1 && count1Cols[col] === 1) {
        result += 1
      }
    }
  }
  
  return result
};
```
