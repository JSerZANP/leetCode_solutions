Youtube video explaining this: https://youtu.be/6EDD1vSSgOk

```js
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number}
 */
var searchInsert = function(nums, target) {
    let start = 0
    let end = nums.length - 1
    
    while (start <= end) {
      const middle = Math.floor((start + end) / 2)
      if (nums[middle] === target) {
        return middle
      } else if (nums[middle] < target) {
        start = middle + 1
      } else {
        end = middle - 1
      }
    }
    // end target start
    return start
};
```
