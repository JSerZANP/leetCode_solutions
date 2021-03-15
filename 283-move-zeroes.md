Here is my video explaining it: https://youtu.be/ex8k9RThrOQ


```js
/**
 * @param {number[]} nums
 * @return {void} Do not return anything, modify nums in-place instead.
 */
var moveZeroes = function(nums) {
    // 1 0 0 3
    // 1 3 0 0 12
    // 1 3 12 0 0
  
  
    // 0 1 0 3 12
    // 12 1 0 3 0
    // 12 1 3 0 0
  
    let positionToSwap = 0
    
    for (let i = 0; i < nums.length; i++) {
      if (nums[i] === 0) continue
      
      ;[nums[i], nums[positionToSwap]] = [nums[positionToSwap], nums[i]]
      positionToSwap += 1
    }
};
```
