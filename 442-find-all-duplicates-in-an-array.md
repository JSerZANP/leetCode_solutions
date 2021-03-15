Here is my video explaining it : https://youtu.be/IUm4KFMiMoQ

```js

/**
 * @param {number[]} nums
 * @return {number[]}
 */
// O(n)
// O(1)
var findDuplicates = function(nums) {
    // [4,3,2,7,8,2,3,1]
    // [7,3,2,4,8,2,3,1]
    // [3,3,2,4,8,2,7,1]
    // [2,3,3,4,8,2,7,1]
    // [3,2,3,4,8,2,7,1]
    // [3,2,3,4,1,2,7,8]
    // [1,2,3,4,3,2,7,8]
  
    // 1. keep swapping to the right position, if same number meets, then duplicate, do nothing
    
  const result = new Set()
  for (let i = 0; i < nums.length; i++) {
    while (nums[i] !== i + 1) {
      // try to swap 
      const rightIndex = nums[i] - 1
      if (nums[rightIndex] === nums[i]) {
        result.add(nums[i])
        break
      } else {
        [nums[i], nums[rightIndex]] = [nums[rightIndex], nums[i]]
      }
    }
  }
  return [...result]
};
```
