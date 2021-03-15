Here is a video explaining this: https://youtu.be/F7dgkLuJV-4

```js
/**
 * @param {number} m
 * @param {number} n
 * @return {number}
 */

// Dynamic programming
// generate the steps for each row
// use 1 array and do the iteration

// Time: O(n * m)
// Space: O(m)
var uniquePaths = function(m, n) {
   const dp = Array(m).fill(1)
   
   while (n > 1) {
     for (let i = 1; i < m; i++) {
       dp[i] += dp[i - 1]
     }
     
     n -= 1
   }

  return dp[m - 1]
};
```
