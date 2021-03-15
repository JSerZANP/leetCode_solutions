My youtube video to explain this: https://youtu.be/SxX8AhuDWic


```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var findLengthOfLCIS = function(nums) {
    if (nums.length === 0) return 0
  
    let max = 1
    
    let currentLength = 1
    for (let i = 1; i < nums.length; i++) {
      if (nums[i] > nums[i - 1]) {
        currentLength += 1
        max = Math.max(currentLength, max)
      } else {
        currentLength = 1
      }
    }
    return max
};
```
