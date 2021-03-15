A video explaining this: https://youtu.be/A95LVX0R5K0

```js
/**
 * @param {number[][]} grid
 * @return {number}
 */

// Time:  O(n * m)
// Space: O(m)
var minPathSum = function(grid) {
    const n = grid.length
   const m = grid[0].length
   // just like 62, we store not the count
   // but [sum, path]
   const dp = Array(m).fill(0).map(_ => Number.POSITIVE_INFINITY)
   dp[0] = 0
  

   
   for (let i = 0; i < n; i++) {
     for (let j = 0; j < m; j++) {
       const left = j === 0 ? Number.POSITIVE_INFINITY : dp[j - 1]
       const top = dp[j]
     
       dp[j] = grid[i][j] + Math.min(left, top)
     }
   }

  return dp[m - 1]
};
```
