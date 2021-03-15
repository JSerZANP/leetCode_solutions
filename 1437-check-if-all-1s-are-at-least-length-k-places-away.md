Me explaining this on youtube: https://youtu.be/6hYEANDwRTw
```js
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {boolean}
 */
// Time: O(n)
// Space: O(1)
var kLengthApart = function(nums, k) {
    let prevOneIndex = -Infinity
    
    for (let i = 0; i < nums.length; i++) {
      if (nums[i] === 1) {
        const distance = i - prevOneIndex - 1
        if (distance < k) {
          return false
        }
        
        prevOneIndex = i
      }
    }
  
  return true
};
```
