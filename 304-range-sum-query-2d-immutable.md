Me explaining it on youtube: https://youtu.be/8caqneyUoWs

```js
/**
 * @param {number[][]} matrix
 */

// Time: O(N)
// Space: O(MN)
var NumMatrix = function(matrix) {
    // sum(i, j, k, l) === sum(0, 0, k, l) - sum(0, 0, i - , l) - sum(0, 0, k, j - 1) + sum(0, 0, i - 1, j - 1)
    const rows = matrix.length
    if (rows === 0) return 0
    const cols = matrix[0].length
    if (cols === 0) return 0
    const sumFromOrigin = Array(rows + 1).fill(0).map(_ => Array(cols + 1).fill(0))
    
    for (let i = 0; i < rows; i++) {
      for (let j = 0; j < cols; j++) {
        const row = i + 1
        const col = j + 1
        sumFromOrigin[row][col] = sumFromOrigin[row][col - 1] - sumFromOrigin[row - 1][col - 1] + sumFromOrigin[row - 1][col] + matrix[i][j]
      }
    }
  
    this.sumFromOrigin = sumFromOrigin
};

/** 
 * @param {number} row1 
 * @param {number} col1 
 * @param {number} row2 
 * @param {number} col2
 * @return {number}
 */

// Time: O(1)
// Space: O(1)
NumMatrix.prototype.sumRegion = function(row1, col1, row2, col2) {
    const sumFromOrigin = this.sumFromOrigin
    return sumFromOrigin[row2 + 1][col2 + 1] - sumFromOrigin[row2 + 1][col1 + 1 - 1] - sumFromOrigin[row1 + 1 - 1][col2 + 1] + sumFromOrigin[row1 + 1 - 1][col1 + 1 - 1]
};

/** 
 * Your NumMatrix object will be instantiated and called as such:
 * var obj = new NumMatrix(matrix)
 * var param_1 = obj.sumRegion(row1,col1,row2,col2)
 */
 ```
