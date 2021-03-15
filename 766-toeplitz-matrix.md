
Me explaining it on youtube: https://youtu.be/Wy_xnTjTxXI


```js
/**
 * @param {number[][]} matrix
 * @return {boolean}
 */

// Time: O(mn)
// Space: O(m + n)
// var isToeplitzMatrix = function(matrix) {
//     //
//     // m - 1, 0, -1, ... -(n - 1)
//     // plus (n - 1)
//     // (m - 1) + (n - 1) , ..... 0
    
//     const rows = matrix.length
//     const cols = matrix[0].length
    
//     const elements = new Array(rows + cols - 1)
    
//     for (let i = 0; i < rows; i++) {
//       for (let j = 0; j < cols; j++) {
//         const index = i - j + cols - 1
        
//         if (elements[index] === undefined) {
//           elements[index] = matrix[i][j]
//         } else if (elements[index] !== matrix[i][j]) {
//           return false
//         }
//       }
//     }
  
//     return true
// };


// compare each row with 1 index shifted

// Time: O(mn)
// space: O(1)
var isToeplitzMatrix = function(matrix) {
    //
    // m - 1, 0, -1, ... -(n - 1)
    // plus (n - 1)
    // (m - 1) + (n - 1) , ..... 0
    
    const rows = matrix.length
    const cols = matrix[0].length
    
    for (let i = 1; i < rows; i++) {
      for (let j = 1; j < cols; j++) {
        if (matrix[i][j] !== matrix[i - 1][j - 1]) {
          return false
        }
      }
    }
  
    return true
};
```
