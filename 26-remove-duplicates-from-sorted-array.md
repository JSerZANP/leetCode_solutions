A video for this problem: https://youtu.be/41PEg1iEZhc

```js
/**
 * @param {number[]} nums
 * @return {number}
 */

// TIME: O(N)
// Space: O(1)
var removeDuplicates = function(nums) {
    let p1 = 0
    let p2 = 0
    
    while (p2 < nums.length) {
      if (nums[p2] !== nums[p2 - 1]) {
        nums[p1] = nums[p2]
        p1 += 1
      }
      
      p2 += 1
    }
  
    return p1
};
```
