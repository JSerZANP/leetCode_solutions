Me explaining this on youtube: https://youtu.be/fVW5pa2JMwA

```js
/**
 * @param {number[]} nums
 * @param {number} limit
 * @return {number}
 */
var longestSubarray = function(nums, limit) {
    // f(i) => longest subarray which ends at i
    // f(i + 1)
    //    = 1 + K: maximum length from i(backword0), for i - K = 1 <= j <= i ,  (j, i + 1) is valid, break at failure or k === f(i)
  
    const longestSubarrayEndsAt = Array(nums.length).fill(1)
    
    let max = 1
    
    for (let i = 1; i < nums.length; i++) {
      const prev = longestSubarrayEndsAt[i - 1]
      let k = i - 1
      while (k >= i - 1 - prev + 1) {
        const diff = Math.abs(nums[i] - nums[k])
        if (diff > limit) {
          break
        }
        
        k -= 1
      }
      
      max = Math.max(max, i - k)
      longestSubarrayEndsAt[i] = i - k
    }
    return max
};
```
