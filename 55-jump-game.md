Youtube explaining this: https://youtu.be/f4mevxUz_mE

```js
/**
 * @param {number[]} nums
 * @return {boolean}
 */
// expand while looping
// Time: O(n) worst
// Space: O(1)
var canJump = function(nums) {
  if (nums.length <= 1) return true
  
  let maxIndex = 0
   
  let i = 0
  
  while (i <= maxIndex) {
    maxIndex = Math.max(maxIndex, i + nums[i])
    
    if (maxIndex >= nums.length - 1) {
      return true
    }
    i += 1
  }
  
  return false
}
```
