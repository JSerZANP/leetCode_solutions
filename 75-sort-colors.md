Here is a video explaining this: https://youtu.be/GBaPjaZ12Qk


```js
/**
 * @param {number[]} nums
 * @return {void} Do not return anything, modify nums in-place instead.
 */
var sortColors = function(nums) {
  // counting + rewrite
  // 2O(n)
  // O(1)
  
  
  // sort method
  // O(nlogn)
  
  
  //  2 0 2 1 1 0
  // 
  
  // Time: O(n)
  // Space: O(1)
  
  let i = 0   // left most index
  let j = nums.length - 1// right most index
  let k = 0   // index to loop
  
  while (k <= j) {
    switch (nums[k]) {
      case 0: // swap it with left most index
        if (k > i) {
          [nums[k], nums[i]] = [nums[i], nums[k]]
        } else {
          k += 1
        }
        i += 1
        break
      case 2: // swap it with right most index
        if (k < j) {
          [nums[k], nums[j]] = [nums[j], nums[k]]
        } else {
          k += 1
        }
        j -= 1
        break
      case 1:
        k += 1
        break
    } 
  }
  
};
```
