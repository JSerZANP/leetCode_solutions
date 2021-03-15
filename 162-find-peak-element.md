Here is my youtube video explaining this: https://youtu.be/RnxuoWbs_v8

```js
/**
 * @param {number[]} nums
 * @return {number}
 */

// Time: O(logn)
// spaceL O(1)
var findPeakElement = function(nums) {
  // binary search
  
  
  //  1 2 3 4
  
  let start = 0
  let end = nums.length - 1
  
  while (start <= end) {
    const middle = Math.floor((start + end) / 2)
    if (nums[middle] < nums[middle + 1]) {
      start = middle + 1
    } else {
      end = middle - 1
    }
  }
  
  // ends when start > end
  return start
};
```
