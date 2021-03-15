Here is a video explaining this: https://youtu.be/8YWIFymZYGA

```js
/**
 * @param {number[][]} grid
 * @return {number}
 */

// Time: O(MN)
// Space: O(1)
var islandPerimeter = function(grid) {
    let result = 0
    
    const rows = grid.length
    if (rows === 0) return result
  
    const cols = grid[0].length
    
    const getPerimeterOfCell = (i, j) => {
      let count = 0
      
      if (grid[i][j] === 0) return count
      
      if (i === 0 || grid[i - 1][j] === 0) count += 1
      if (i === rows - 1 || grid[i + 1][j] === 0) count += 1
      if (j === 0 || grid[i][j - 1] === 0) count += 1
      if (j === cols - 1 || grid[i][j + 1] === 0) count += 1
      
      return count
    }
    
    for (let i = 0; i < rows; i++) {
      for (let j = 0; j < cols; j++) {
        result += getPerimeterOfCell(i, j)
      }
    }
    
    return result
};
```
