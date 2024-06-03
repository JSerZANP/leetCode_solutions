```js
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number}
 */
var search = function (nums, target) {
  let i = 0;
  let j = nums.length - 1;
  while (i <= j) {
    const m = Math.floor((i + j) / 2);
    if (nums[m] === target) {
      return m;
    }
    if (nums[m] < target) {
      i = m + 1;
    } else {
      j = m - 1;
    }
  }
  // when it stops i should be where the target should be at
  return -1;
};
```
