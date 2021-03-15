Here is my youtube video to explain this: https://youtu.be/W2c5NjpEnX8
```js
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number}
 */
var threeSumSmaller = function(nums, target) {
  // brute force O(N^3) 
  
  // 1. sort first O(nlogn)
  // 2. first the left number => 2 sum problem O(n) => O(n^2)
  
  if (nums.length < 3) return 0
  
  nums.sort((a, b) => a - b)
  
  let result = 0
  // -2 0 0 2 2 
  for (let i = 0; i + 2 < nums.length; i++) {
    let start = i + 1
    let end = nums.length - 1
    while (start < end) {
      const sum = nums[i] + nums[start] + nums[end]
      if (sum < target) {
        result += end - start
      }
      
      if (sum < target) {
          start += 1
      } else {
          end -= 1
      }
    }
  }
      
  return result
};
```
