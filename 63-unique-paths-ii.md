A video explaining this: https://youtu.be/guMv7BKIKCg

```js
/**
 * @param {number[][]} obstacleGrid
 * @return {number}
 */
// Time: O(n * m)
// Space: O(m)
var uniquePathsWithObstacles = function(obstacleGrid) {
  
    const n = obstacleGrid.length
    const m = obstacleGrid[0].length
   const dp = Array(m).fill(0)
   dp[0] = 1
   
   for (let i = 0; i < n; i++) {
     for (let j = 0; j < m; j++) {
       // only update when it is empty
       if (obstacleGrid[i][j] === 0) {
         dp[j] += j > 0 ? dp[j - 1] : 0
       } else {
         dp[j] = 0
       }
     }
   }

  return dp[m - 1]
};
```
