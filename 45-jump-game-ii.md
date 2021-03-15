A video explaining this: https://youtu.be/NgZrnWZIEkA

```js
/**
 * @param {number[]} nums
 * @return {number}
 */
// Time: O(n^2)
var jump = function(nums) {
  if (nums.length === 1) return 0
  
  const dp = Array(nums.length).fill(Number.POSITIVE_INFINITY)
  
  dp[0] = 0
  
  // [3,3,2,1,1,4]
  // [0]
  // [0, 1, 1, 1]
  // [0, 1, 2, 2, 2]
  for (let i = 0; i < nums.length; i++) {
    if (i > 0 && i + nums[i] <= i - 1 + nums[i - 1]) {
      continue
    }
    for (let k = i + 1; k <= i + nums[i] && k < nums.length; k++) {
      dp[k] = Math.min(dp[k], dp[i] + 1)
      if (k === nums.length - 1) {
        return dp[k]
      }
    }
  }
};
```
