A video explaining this: https://youtu.be/PTLuyqH2VkM
```js
/**
 * @param {number[]} nums
 * @param {number} val
 * @return {number}
 */
var removeElement = function(nums, val) {
    let p1 = 0
    let p2 = 0
    
    while (p2 < nums.length) {
      if (nums[p2] !== val) {
        nums[p1] = nums[p2]
        p1 += 1
      }
      
      p2 += 1
    }
  
    return p1
};
```
