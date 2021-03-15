Me explaining this on youtube: https://youtu.be/CBediynjFxE
```js
/**
 * @param {number[][]} grid
 * @return {number}
 */

// Time: worst (m * n)!
// space: O(m * n + m * n) => O(m * n)
var getMaximumGold = function(grid) {
    // use flag to keep track of the availitity of each cells
    const isAvaiable = grid.map(row => row.map(cell => cell !== 0))
    
    let max = 0
    
    let sum = 0
    
    const rows = grid.length
    const cols = grid[0].length
    // recursion try to choose a cell
    const walk = (i, j) => {
        if (i < 0 || i > rows - 1  || j < 0 || j > cols - 1 || !isAvaiable[i][j]) return
        
        // add to sum
        sum += grid[i][j]
        
        // update max
        max = Math.max(sum, max)
        
        // update availibity
        isAvaiable[i][j] = false
        
        // walk around
        walk(i, j + 1)
        walk(i + 1, j)
        walk(i, j - 1)
        walk(i - 1, j)
        
        // update sum
        sum -= grid[i][j]
        
        // update availibity 
        isAvaiable[i][j] = true
    }
    
    // start on all the possible gold cell
    grid.forEach((row, i) => {
        row.forEach((cell, j) => walk(i, j))
    })
    
    return max
};
```
