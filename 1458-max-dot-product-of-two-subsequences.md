
Here is me explaining on youtube: https://youtu.be/M39Ap4euAQI

```js
/**
 * @param {number[]} nums1
 * @param {number[]} nums2
 * @return {number}
 */
// m n
// O(m ^ 2 * n)
// O(m n)
var maxDotProduct = function(nums1, nums2) {
    // [2,1,-2,5] [3,0,-6]
    // product(i, j) = 
    //    if nums2[j] is not used, product(i, j - 1)
    //    if nums2[j] is used,  max {
    //             0<= k <= i, nums2[j] * nums1[k] + max(0, product[k - 1][j - 1]) 
    //    }
    const length1 = nums1.length
    const length2 = nums2.length
    const dp = new Array(length1).fill(0).map(_ => new Array(length2))
    
    for (let i = 0; i < length1; i++) {
      for (let j = 0; j < length2; j++) {
        if (i === 0 && j === 0) {
          dp[i][j] = nums1[i] * nums2[j]
        } else if (i === 0) {
          dp[i][j] = Math.max(dp[i][j - 1], nums1[i] * nums2[j])
        } else if (j === 0) {
          dp[i][j] = Math.max(dp[i - 1][j], nums1[i] * nums2[j])
        } else {
          let maxProductIfUsed = -Infinity
          for (let k = i; k >= 0; k--) {
            maxProductIfUsed = Math.max(
              maxProductIfUsed,
              nums1[k] * nums2[j] + Math.max(0, k > 0 ? dp[k - 1][j - 1] : 0)
            )
          }
          
          dp[i][j] = Math.max(maxProductIfUsed, dp[i][j - 1])
        }
      }
    }
    return dp[length1 - 1][length2 - 1]
};
```
