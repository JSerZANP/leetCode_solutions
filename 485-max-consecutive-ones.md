My youtube explaining video: https://youtu.be/D6GnFWfs7c8


```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var findMaxConsecutiveOnes = function(nums) {
  // 1,1,0,1,1,1  
  // 1 1 0 1 1 1
  
  // keep track of the non-1 right before the start of several 1s
  
  let prev = -1
  let result = 0
  for (let i = 0; i < nums.length + 1; i++) {
    if (nums[i] !== 1) {
      result = Math.max(result, i - prev - 1)
      prev = i
    }
  }
  return result
};
```
